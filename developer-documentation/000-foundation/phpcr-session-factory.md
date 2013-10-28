# PHPCR Session Factory

Manages PHPCR Sessions.

##Configuration

Parameter:

    phpcr_factoryClass: Jackalope\RepositoryFactoryJackrabbit
    phpcr_url: http://localhost:8080/server
    phpcr_username: admin
    phpcr_password: admin
    
Usage:

service:

    sulu_content.mapper:
        class: %sulu_content.mapper.class%
        arguments: ["@sulu_core.phpcr.session"]
        
php:

    $sessionFactory->getSession()
