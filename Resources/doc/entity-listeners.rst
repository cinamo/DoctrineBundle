Entity Listeners
================

Entity listeners that are services must be registered with the entity
listener resolver. You can tag your entity listeners and they will automatically
be added to the resolver. Use the entity_manager attribute to specify which
entity manager it should be registered with. Example:

.. configuration-block::

    .. code-block:: yaml

        services:
            user_listener:
                class: \UserListener
                tags:
                    - { name: doctrine.orm.entity_listener }
-
                        name: doctrine.orm.entity_listener
                        event: preUpdate
                        entity: App\Entity\User
                        entity_manager: custom
    .. code-block:: xml

        <?xml version="1.0" ?>

        <container xmlns="http://symfony.com/schema/dic/services"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

            <services>
                <service id="user_listener" class="UserListener">
                    <tag name="doctrine.orm.entity_listener" event="preUpdate" entity="App\Entity\User" />
                    <tag
                        name="doctrine.orm.entity_listener"
                        event="preUpdate"
                        entity="App\Entity\User"
                        entity_manager="custom"
                    />                </service>
            </services>
        </container>

If you use a version of doctrine/orm < 2.5 you have to register the entity listener in your entity as well:

.. code-block:: php

    <?php
    // User.php

    use Doctrine\ORM\Mapping as ORM;

    /**
     * @ORM\Entity
     * @ORM\EntityListeners({"UserListener"})
     */
    class User
    {
        // ....
    }

See also
https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/events.html#entity-listeners
for more info on entity listeners and the resolver required by Symfony.
