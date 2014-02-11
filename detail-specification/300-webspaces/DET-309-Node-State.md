# DET 309 Node State

## ContentMapper

Last Optional Parameter is state (default for new nodes TEST, default for other ignore it)

```
    public function save(
        $data,
        $templateKey,
        $webspaceKey,
        $languageCode,
        $userId,
        $partialUpdate = true,
        $uuid = null,
        $parentUuid = null,
        $state = null
    );
```

## States

* TEST (INT => 1)
* PUBLISHED (INT => 2)

Default = TEST

__CONTENTS__ node is default PUBLISHED and no transitions allowed (ignored)

## Transition

| FROM | TO | RESULT |
| --- | --- | --- |
| TEST | PUBLISHED | OK |
| PUBLISHED | TEST | Exception |
| - | TEST / PUBLISHED | OK|

## Inheritance

```
  contents
     |
     a
   -- --
  |     |
  b     c
 - -
|   |
d   e
```

* Startup:
	* Everything is TEST for default
* d.state = published
	* Everything is TEST (d inherite state of b)
* b.state = published
	* Everything is TEST (b inherite state of a)
* a.state = published
	* a, b, d = PUBLISHED
	* c, e = TEST
* b.state = TEST && c.state = PUBLISHED
	* a, c = PUBLISHED
	* b, d, e = TEST
	
State is inherited from parent: if he is TEST all descendent node are TEST. If he is PUBLISHED each node has its own state.