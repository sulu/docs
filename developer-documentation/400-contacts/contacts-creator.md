# How to deal with idContactsCreator and idContactsChanger

* set onDelete to "set null" => this will set i null when the contact is deleted.

## Example

    creator:
        targetEntity: Contact
        joinColumn:
            name: idContactsCreator
            referencedColumnName: id
            nullable: true
            onDelete: "set null"
    changer:
        targetEntity: Contact
        joinColumn:
            name: idContactsChanger
            referencedColumnName: id
            nullable: true
            onDelete: "set null"
