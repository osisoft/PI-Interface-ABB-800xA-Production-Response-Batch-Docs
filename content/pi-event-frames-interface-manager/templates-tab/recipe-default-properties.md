---
uid: BIF_RecipeDefaultProperties
---

# Recipe templates default properties

<!-- Topic requires customization for specific interface (ABB PR) -->

## Batch Level
The following are the recipe template default values for the BATCH level:

| Template | Default
| ----- | ----- |
| Name | [Procedure] 
| Batch ID | [BatchID]
| Product | [Product] |
| Category | OSIBatch |
| Template | Procedure |
| Module Path [0] | [UNIT] |
| Module Path [1] | [UNIT2] |
| Module Path [2] | [UNIT3] |
| Module Path [3] | [UNIT4] |
| Module Path [4] | [UNIT5] |

**Default Properties**

[RECIPE]

The index in the recipe template heirarchy corresponds to the RECIPE item default property (1).

      Recipe[1].DEFAULTPROPERTY[1].NAME = Recipe
      Recipe[1].DEFAULTPROPERTY[1].VALUE = [RECIPENAME]

[PRODUCT]

The index in the recipe template heirarchy corresponds to the PRODUCT item default property (2).

      Product[2].DEFAULTPROPERTY[2].NAME = Product
      Product[2].DEFAULTPROPERTY[2].VALUE = [PRODUCT]

## Unit Batch Level
The following are the recipe template default values for the UNIT BATCH level:

| Template | Default
| ----- | ----- |
| Name | [UnitProcedure] 
| Batch ID | [BatchID]
| Product | [Product] |
| SearchByStartTime | true |
| SearchByEndTime | true |
| Category | OSIBatch |
| Template | UnitProcedure |
| Module Path [0] | [UNIT] |
| Module Path [1] | [UNIT2] |
| Module Path [2] | [UNIT3] |
| Module Path [3] | [UNIT4] |
| Module Path [4] | [UNIT5] |

**Default Properties**

[PROCEDURE] = 3

      .NAME = PROCEDURE
      .VALUE = [UNITPROCEDURE|OPERATION|Phase|PhaseState|PhaseStep]

[PRODUCT] = 2

      .NAME = Product
      .VALUE = [Product]

[RECIPE] = 1

      .NAME = BatchID
      .VALUE = [BatchID]

## Operation Level
The following are the recipe template default values for the OPERATION level:

| Template | Default
| ----- | ----- |
| Name | [Operation] 
| Category | OSIBatch |
| Template | Operation |

## Phase Level
The following are the recipe template default values for the PHASE level:

| Template | Default
| ----- | ----- |
| Name | [Phase] 
| Category | OSIBatch |
| Template | Phase |

## Phase State Level
The following are the recipe template default values for the PHASE STATE level:

| Template | Default
| ----- | ----- |
| Name | [PhaseState] 
| Category | OSIBatch |
| Template | PhaseState |

## Phase Step Level
The following are the recipe template default values for the PHASE STEP level:

| Template | Default
| ----- | ----- |
| Name | [PhaseStep] |
| Category | OSIBatch |
| Template | PhaseStep |

## Unit State Level
The following are the recipe template default values for the UNIT STATE level:

| Template | Default
| ----- | ----- |
| Name | [UnitState] |
| Category | OSIBatch |
| Template | UnitState |
| SearchByEndTime | false |
| Module Path | [UNIT] |


