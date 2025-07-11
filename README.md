## Project Info

Project Name: Where Am I? <br>
Platform: PC ONLY<br>
Built with: Unreal Engine 4<br><br>
Systems: <br>
1. Health and Stamina System
2. Inventory System
3. Save/Load System (TO DO)

***


## **Architechture:**

<pre>
├── .
└── └── Content/
    ├── ├── /Blueprints/
    ├── │   ├── /Components
    ├── │   ├── /Data
    ├── │   ├── /Health
    ├── │   ├── /Widgets
    ├── │   └── /Inventory
    ├── └── /Player/
    │   └── └── /Blueprints/
    │       ├── ├── /BP_ThirdPersonCharacter
    │       └── └── /ThirdPersonGameMode
    ├── /Mannequin (Taken from the content pack (ThirdPersonCharacter))
    └── /Maps  </pre>


## **The Big Picture?**

- As we're using ThirdPersonCharacter content pack from UE, We have our player ready with Walk/Run/Idle/Jump features + animations.
- However, when our player runs/sprints he loses stamina, if all stamina is lost, then the player starts losing health as well...

- To help our player regain his health back, we are placing eatables / collectible items into the world and so
our player has the functionality to pick items into inventory


# **Documentation**


1. Health - Stamina System Implementation
- BP_HealthComponent:
    - Functions:
       * DecreaseHealth
       * GetPlayerHealth
       * DecreaseStamina
       * IncreaseStamina
       * GetPlayerStamina

    - Variables:
       * HealthUI -> Reference to HealthUI
       * StaminaUI -> Reference to StaminaUI

- BP_GameManager
   - BP_HealthComponent is BP_GameManager's component and so, It is BP_GameManager that binds to events of Player and calls HealthComponent's functions.

2. Inventory System Implementation
     - Structures:
         * ST_Items
     - Data Tables:
         * DT_Items (This data table has all the items that can be placed into the world)
     - Blueprints:
         - BP_Item:
             - Variables:
                 * Item Info `ST_Items`
         - BP_ItemPlacer:
             - Variables:
                 * ItemsToPlace `int`
             - Functions:
                 * PlaceItems
                 * GetRandomItem
                 * GetRandomLocation
                 * SetPlacedItemInformation (Sets the mesh of our newly placed item, and also sets it's variable Item Info from (BP_Items) with info from GetRandomItem function.
         - BP_InventoryManager:
             - Variables:
                 * bCanPickItem `bool`
                 * bIsHandEmpty `bool`
                 * IsInventoryOpened `bool`
                 * ItemsInHand `string[]`
                 * GameManager_BP `BP_GameManager`'s ref
                 * Item_BP `BP_Item`'s ref
                 * InventoryGridMaxRC (stores the max row column so the inventory items dont exceed the limit)
                 * CurrentInventoryGridRC (stores the last added item's grid row-column

             - Functions:
                 * DisplayItemPickablity (Shows E on screen)
                 * HideItemPickablitity (Hides E from screen)
                 * PickItem
                 * DropItem
                 * ToggleInventoryOpenClose (closes/opens UI widget)
                 * AddItemInInventory
                 * SetMaxRowColumnInventory
                 * GetNewRowColumn (We're using Grid to store our inventory items, so row column is must for each added item)






