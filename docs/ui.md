# UI Builder
## Opening Joget Test App
If the App is not visible in the dashboard follow [View App Procedure](../docs/forms.md#opening-joget-test-app).

## Create and Edit UI
Create a new **UI** through UI Builder navigation item or through the **App Composer** screen.

There is a difference between inserting a **Run Process** item and the individual **Form** (where the form is submitted without actions afterwards) or **List** (where a list is displayed) items.

## Digital Registry UI

![Digital Registry UI](../assets/img/components/UI/digital-registry/DigitalRegistry.png)

The Digital Registry UI consists of several default side navigation items + 3 custom ones connected to Digital Registry BB Emulator (DR):
1. Emulator's DB list of people
2. Create new person in the Digital Registry's DB
3. Update person in Digital Registry's DB

#### Digital Registry List
![Digital Registry List](../assets/img/components/UI/digital-registry/DigitalRegistryList.png)

Drag and drop **List** element from the navigation menu to insert the list to the main screen.
Configure the list to point to the [Digital Registry List](../docs/lists.md#digital-registry-bb-emulator-list) through the **List** property on the right side (after list is clicked).

#### Create new person in Digital Registry

![Digital Registry Create New Person](../assets/img/components/UI/digital-registry/DigitalRegistryCreateNew.png)

Drag and drop **Form** element into the main screen. Configure the [Form](../docs/forms.md) to be [Create New Person](../docs/forms.md#create-new-person). Edit the form's label as well.

Edit the **Message after submission** as preferred.
![Create New Person Success Message](../assets/img/components/UI/digital-registry/DigitalRegistryCreateNewMessage.png)

#### Update person's details in Digital Registry

![Digital Registry Update Person](../assets/img/components/UI/digital-registry/DigitalRegistryUpdate.png)

Drag and drop **Run Process** element into the main screen. Configure the [Process](../docs/process.md) to be [Update Person Data](../docs/forms.md#update-person).

Edit the **Submit Button Label** as preferred and check **Run Process Without Confirmation Screen?** if wanted.

![Update Process Configuration](../assets/img/components/UI/digital-registry/DigitalRegistryConfigureProcess.png)

### Digital Registry Beneficiaries
![Digital Registry Beneficiaries UI](../assets/img/components/UI/digital-registry/DigitalRegistryBeneficiaries.png)

This UI consists of four types of items:
1. Form
2. List
3. Process
4. Inbox

Drag and drop **Form, List, Process or Inbox** element from the navigation menu to insert into to the main screen.
Configure the items to point to the appropriate forms, list, process or assignment  (for the Inbox) through the corresponding property on the right side of the item (after the component is clicked).

#### Beneficiary Form
![Register Beneficiary](../assets/img/components/UI/beneficiary/BeneficiaryForm.png)

#### Beneficiary List
![Beneficiaries List](../assets/img/components/UI/beneficiary/BeneficiaryList.png)

#### Validate Beneficiary
![Validate Beneficiary](../assets/img/components/UI/beneficiary/ValidateBeneficiary.png)

#### Beneficiary Validation Form Submission History
![Validate beneficiaries process](../assets/img/components/UI/beneficiary/BeneficiaryValidationHistory.png)

UIs can be previewed with data coming from the datasource directly in **Preview** tab or through the **Launch** button in the top right corner.

### It is recommended to click **Apply Change** after every change made and click Save button in the top right corner to save the progress otherwise it may be lost!