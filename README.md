# apache-atlas-custom-type

## Overview
This repository contains JSON templates that can be executed on the Apache Atlas API for creation of custom type defintions 


## Excel Model Example

This folder contains
```bash

1. full_model [folder] --> which contains artifacts to create the final model in Apache Atlas.

2. person_entity_def.json --> person_entity_def.json

```


## Excel Model Definition

Below is the example of our model. We have a system instance called `cp_system` that is owned by a person (aka `cp_person`) and contains folders of type `cp_folder` where we store files of type `cp_files`, each of which includes worksheets of type `cp_worksheet` that enable us to store tabular data with columns of type `cp_column`. The entities are also connected, giving each link a different name.

  

```mermaid
classDiagram

Referenceable <|-- cp_system~Infrastructure~ : Inheritance

cp_system "*" --> "1" cp_person : end1->systemOwner<br> end2->ownerToSystems

cp_folder~DataSet~ "*" --> "1" cp_person : end1->folderOwner<br> end2->ownerToFolders

cp_folder "*" --> "1" cp_system : end1->folderInSystem<br> end2->systemFolders

cp_file~DataSet~ "*" --> "1" cp_person : end1->fileOwner<br> end2->ownerToFiles

cp_file "*" --> "1" cp_folder~DataSet~ : end1->filesInFolder<br> end2->folderOfFile

cp_worksheet~DataSet~ --* cp_file : end1->worksheetsInFile<br> end2->fileOfWorksheet

cp_column~DataSet~ --* cp_worksheet: end1->columnsInWorksheet<br> end2->columnOfWorksheet

  

cp_folder~DataSet~ --|> Referenceable: Inheritance

cp_file~DataSet~ --|> Referenceable: Inheritance

cp_worksheet~DataSet~ --|> Referenceable: Inheritance

cp_column~DataSet~ --|> Referenceable: Inheritance

cp_person --|> Referenceable: Inheritance

%% cp_system --|> Referenceable: Inheritance

class Referenceable{

String qualifiedName$

}

class cp_system{

+String name

+String address

+String IP

+systemFolders(List~cp_folder~)

+systemOwner(cp_person)

}

class cp_person{

+String name

+String email

+ownerToFolders(List~cp_folder~)

+ownerToFiles(List~cp_file~)

+ownerToSystems(List~cp_system~)

}

class cp_folder{

+String name

+folderOwner(cp_person)

+filesInFolder(List~cp_file~)

+folderInSystem(cp_system)

}

class cp_file{

+String name

+String size

+String fileType

+String filePermission

+fileOwner(cp_person)

+worksheetsInFile(List~cp_worksheet~)

+folderOfFile(cp_folder)

}

class cp_worksheet{

+String name

+String sheetDescription

+columnsInWorksheet(cp_column)

+fileOfWorksheet(cp_file)

}

class cp_column{

+String name

+String columnDescription

+bool isMandatory

+bool isKey

+String keyType

+columnOfWorksheet(cp_column)

}
```

  

## What's next
Once the model is created, we need to push data using rest API interface. We can learn more about them on the blog post itself.s to create the final model in Apache Atlas. 
Person Entity Definition.json
```

## Excel Model Definition

Below is the example of our model. We have a system instance called `cp_system` that is owned by a person (aka `cp_person`) and contains folders of type `cp_folder` where we store files of type `cp_files`, each of which includes worksheets of type `cp_worksheet`  that enable us to store tabular data with columns of type `cp_column`. The entities are also connected, giving each link a different name.

```mermaid
classDiagram
    Referenceable <|-- cp_system~Infrastructure~ : Inheritance
    cp_system "*" --> "1" cp_person : end1->systemOwner<br> end2->ownerToSystems
    
    cp_folder~DataSet~ "*" --> "1" cp_person : end1->folderOwner<br> end2->ownerToFolders
    cp_folder "*" --> "1" cp_system : end1->folderInSystem<br> end2->systemFolders
    cp_file~DataSet~ "*" --> "1"  cp_person : end1->fileOwner<br> end2->ownerToFiles
    cp_file "*" --> "1" cp_folder~DataSet~ :  end1->filesInFolder<br> end2->folderOfFile
    cp_worksheet~DataSet~ --* cp_file : end1->worksheetsInFile<br> end2->fileOfWorksheet
    cp_column~DataSet~ --* cp_worksheet: end1->columnsInWorksheet<br> end2->columnOfWorksheet

    cp_folder~DataSet~ --|>  Referenceable: Inheritance
    cp_file~DataSet~ --|>  Referenceable: Inheritance
    cp_worksheet~DataSet~ --|>  Referenceable: Inheritance
    cp_column~DataSet~ --|>  Referenceable: Inheritance
    cp_person --|>  Referenceable: Inheritance
    %% cp_system --|>  Referenceable: Inheritance
    class Referenceable{
        String qualifiedName$ 
    }
    
    class cp_system{
        +String name
        +String address
        +String IP
        +systemFolders(List~cp_folder~)
        +systemOwner(cp_person)
    }
    class cp_person{
        +String name
        +String email
        +ownerToFolders(List~cp_folder~)
        +ownerToFiles(List~cp_file~)
        +ownerToSystems(List~cp_system~)
    }
    class cp_folder{
        +String name
        +folderOwner(cp_person)
        +filesInFolder(List~cp_file~)
        +folderInSystem(cp_system)
    }
    class cp_file{
        +String name
        +String size
        +String fileType
        +String filePermission
        +fileOwner(cp_person)
        +worksheetsInFile(List~cp_worksheet~)
        +folderOfFile(cp_folder)
    }
    class cp_worksheet{
        +String name
        +String sheetDescription
        +columnsInWorksheet(cp_column)
        +fileOfWorksheet(cp_file)
    }
     class cp_column{
        +String name
        +String columnDescription
        +bool isMandatory
        +bool isKey
        +String keyType
        +columnOfWorksheet(cp_column)
    }   
```

## What's next

Once the model is created, we need to push data using rest API interface. We can learn more about them on the blog post itself.
