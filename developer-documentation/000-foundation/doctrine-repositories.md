# Doctrine Repositories #

* Use query builder by default
* Use setHint() method to prevent auto loading of referenced tables - this way only specified tables will be loaded
* Example:

```
use Doctrine\ORM\Query;
```

```
$qb = $this->createQueryBuilder('user')
    ->leftJoin('user.userRoles', 'userRoles')
    ->leftJoin('userRoles.role', 'role')
    ->leftJoin('user.contact', 'contact')
    ->leftJoin('contact.emails', 'emails')
    ->addSelect('userRoles')
    ->addSelect('role')
    ->addSelect('contact')
    ->addSelect('emails')
    ->where('user.contact=:contactId');

$query = $qb->getQuery();
$query->setHint(Query::HINT_FORCE_PARTIAL_LOAD, true);
$query->setParameter('contactId', $id);

return $query->getSingleResult();
```
