# Swift-Data
> Working with persistence

## 1 - Create struct to save model (Optional)

```swift
struct Person{
	var name:String
	var age:Int
}
```

## 2  - Create DataBase file

- File > New > File > Data Model
- Create an Entity by each Model
- Creare Attribute Inside Entity ```PersonEntity```

## 3 - Create Database Controller

Dependency: Import CoreData

Create Class like ```DataController``` with inheritance ```ObservableObject```

```swift
import Fundation
import CoreData

class DataController: ObservableObject{
	let container = NSPersistentContainer(name: "DB NAME")
	
	init(){
		container.loadPersistentStores{ description, error
			if let e = error{
				print("Error to load database")
			}
		}
	}
}
```

## 4 - Instance Database Controller in the Home of app, set like environment

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
```

## 5 - Use Entity on child views

```swift
struct ContentView: View{
	// To manage data environment
	@Environment(\.managedObjectContext) var moc
	
	// Return array with all entities inside on PersonEntity
	@FetchRequest(sortDescriptors: []) var persons: FetchedResults<PersonEntity>
	
	var body: some View{
		List(persons){ person in
			Text(person.name ?? "Unknown")
		}
		
		// Add Person
		Button("Add Person"){
			var set = PersonEntity(context: moc)
			set.id = UUID()
			set.name = "John Doe"
			set.age = Int16(18)
			
			// Persistence
			try? mod.save()
		}
	}


