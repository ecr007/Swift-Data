# Swift-Data
> Working with persistence

## 1 - Create struct to save model

```swift
struct Person{
  var name:String
  var age:Int
}
```

## 2  - Create DataBase file

1 - File > New > File > Data Model
2 - Create an Entity by each Model

## 3 - Create Database Controller

Dependency: Import CoreData

Create Class like ```DataController``` with inheritance ```ObservableObject```

## 4 - Instance Database Controller in the Home of app

```swift
import SwiftUI

@main
struct HomeView: App{
  @StateObject var dataController:DataController = DataController()
  
  var body: some Scene{
    WindowGroup{
      ContentView()
        .environment(\.managedObjectContext,dataController.container.viewContext)
    }
  }

}

