# Custom-Object-Duplicate-Merge-LWC

https://github.com/Mihir-Dhore/Custom-Object-Duplicate-Merge-LWC/assets/83826641/ff4e2a62-aeb9-4d97-bdee-ef247c2dbf8d



HTML:-

```
<template>
    <lightning-card title="Duplicate Merge" variant="base">
        <div class="slds-p-around_medium">
            <button onclick={showButtonData}>Show Data</button>
            <button class="slds-m-around_small" onclick={handleMergeData}>Merge Data</button>
        </div>

        <template if:true={showDuplicateRecords}>
            <div class="slds-p-around_medium">
                <lightning-datatable data={showData} draft-values={draftValues} onrowselection={handleRowSelection}
                    max-row-selection=1 onsave={handleSave} columns={columns} key-field="Id">
                </lightning-datatable>
            </div>
        </template>


        <!-- Merge Data -->
        <template if:true={showMergeData}>
            <section role="dialog" tabindex="-1" aria-modal="true" aria-labelledby="modal-heading-01"
                class="slds-modal slds-fade-in-open slds-modal_large">
                <div class="slds-modal__container">
                    <button class="slds-button slds-button_icon slds-modal__close slds-button_icon-inverse">
                        <svg class="slds-button__icon slds-button__icon_large" aria-hidden="true">
                            <use xlink:href="/assets/icons/utility-sprite/svg/symbols.svg#close"></use>
                        </svg>
                        <span class="slds-assistive-text">Cancel and close</span>
                    </button>
                    <div class="slds-modal__header">
                        <h1 id="modal-heading-01" class="slds-modal__title slds-hyphenate">Merge Record</h1>
                    </div>
                    <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">

                        <template if:true={showMergeData}>
                            <table class="slds-table slds-table_cell-buffer slds-table_bordered">
                                <thead>
                                    <tr class="slds-line-height_reset">
                                        <th class="" scope="col">
                                            <div class="slds-truncate" title="Select Master">
                                                Fields
                                            </div>
                                        </th>
                                        <th class="" scope="col">
                                            <div class="slds-truncate" title="Select Current Record">
                                                Current Record
                                            </div>
                                        </th>
                                        <th class="" scope="col">
                                            <div class="slds-truncate" title="Select Selected Record">
                                                Selected Record
                                            </div>
                                        </th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <template for:each={mergedData} for:item="item">
                                        <tr key={item.field} class="slds-hint-parent">
                                            <td data-label="Field">
                                                <div class="slds-truncate" title={item.field} id={item.field}>
                                                    {item.field}
                                                </div>
                                            </td>
                                            <td data-label="Record 1">
                                                <div class="slds-truncate" title={item.cr}>
                                                    <input type="radio" value={item.cr} name={item.field}
                                                        onchange={getRadioBoxValueCR} checked={item.cr}>{item.cr}
                                                </div>
                                            </td>
                                            <td data-label="Record 2">
                                                <div class="slds-truncate" title={item.record2Field}>
                                                    <input type="radio" value={item.sr} name={item.field}
                                                        onchange={getRadioBoxValue}
                                                        checked={item.isRecord2FieldSelected}>{item.sr}
                                                </div>
                                            </td>
                                        </tr>
                                    </template>
                                </tbody>
                            </table>
                        </template>
                    </div>
                    <div class="slds-modal__footer">
                        <button class="slds-button slds-button_neutral" onclick={handleModalCancel}
                            aria-label="Cancel and close">Cancel</button>
                        <button class="slds-button slds-button_brand" onclick={handleModalMerge}>Merge</button>
                    </div>
                </div>
            </section>
            <div class="slds-backdrop slds-backdrop_open" role="presentation"></div>


            <!-- <section role="dialog" tabindex="-1" aria-modal="true" aria-labelledby="modal-heading-01"
                class="slds-modal slds-fade-in-open">
                <div class="slds-modal__container">
                    <button class="slds-button slds-button_icon slds-modal__close slds-button_icon-inverse">
                        <svg class="slds-button__icon slds-button__icon_large" aria-hidden="true">
                            <use xlink:href="/assets/icons/utility-sprite/svg/symbols.svg#close"></use>
                        </svg>
                        <span class="slds-assistive-text">Cancel and close</span>
                    </button>
                    <div class="slds-modal__header">
                        <h1 id="modal-heading-01" class="slds-modal__title slds-hyphenate">Modal header</h1>
                    </div>
                    <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">

                        <div class="c-container">
                            <lightning-layout horizontal-align="space">
                                <lightning-layout-item padding="around-small">
                                    <div class="custom-box">
                                        <h2 class="slds-align_absolute-center slds-p-bottom_small">Fields</h2>
                                        <template for:each={storeFieldNamesss} for:item="fieldNamess">
                                            <div key={fieldNamess.Id} class="slds-p-around_small  ">
                                                <span> {fieldNamess}</span>
                                            </div>
                                        </template>
                                    </div>
                                </lightning-layout-item>
                                <lightning-layout-item padding="around-small">
                                    <div class="custom-box">
                                        <h2 class="slds-align_absolute-center slds-p-bottom_small">Current Record</h2>
                                        <template for:each={storeCurrentRecData} for:item="currentRec">
                                            <div key={currentRec.Id} class="slds-p-around_small  ">
                                                <span>{currentRec}</span>
                                            </div>
                                        </template>
                                    </div>
                                </lightning-layout-item>
                                <lightning-layout-item padding="around-small">
                                    <div class="custom-box">
                                        <h2 class="slds-align_absolute-center slds-p-bottom_small">Current Record</h2>
                                        <template for:each={storeSelectedRecData} for:item="selectedRec">
                                            <div key={selectedRec.Id} class="slds-p-around_small  ">
                                                <span>{selectedRec}</span>
                                            </div>
                                        </template>
                                    </div>
                                </lightning-layout-item>

                            </lightning-layout>
                        </div>
                    </div>
                    <div class="slds-modal__footer">
                        <button class="slds-button slds-button_neutral" onclick={handleModalCancel}
                            aria-label="Cancel and close">Cancel</button>
                        <button class="slds-button slds-button_brand" onclick={handleModalMerge}>Save</button>
                    </div>
                </div>
            </section>
            <div class="slds-backdrop slds-backdrop_open" role="presentation"></div> -->
        </template>

    </lightning-card>
</template>
```

JS:-

```
import { LightningElement, track,api,wire } from 'lwc';
import getSObjectFieldsQuery from '@salesforce/apex/customObjectDuplicateClass.getSObjectFieldsQuery';
import { updateRecord } from 'lightning/uiRecordApi';
import { ShowToastEvent } from 'lightning/platformShowToastEvent';
import getSObjectFields from '@salesforce/apex/customObjectDuplicateClass.getSObjectFields';
import mergeRecord from '@salesforce/apex/customObjectDuplicateClass.mergeRecord';
import getCurrentRecord from '@salesforce/apex/customObjectDuplicateClass.getCurrentRecord';
import getCurrentObjectRecordNameAndEmail from '@salesforce/apex/customObjectDuplicateClass.getCurrentObjectRecordNameAndEmail';
import deleteMergedRecord from '@salesforce/apex/customObjectDuplicateClass.deleteMergedRecord';

// import { getObjectInfo } from 'lightning/uiObjectInfoApi';

import getAllChildRecordsAndUpdate from '@salesforce/apex/customObjectDuplicateClass.getAllChildRecordsAndUpdate';

const columns = [
    { label: 'Name', fieldName: 'Name', type: 'text',editable: true,},
    {label: 'Email', fieldName: 'Email__c', type: 'email',editable: true,}
];


export default class CustomObjectDuplicateRecordMergeDynamically extends LightningElement {

    // connectedCallback(){
    //     this.wiredObjectInfo();
    // }

    // @track options;
    // @track RelatedObjectData = [];
    // @wire(getObjectInfo, { objectApiName: '$objectApiName' })
    // wiredObjectInfo({ error, data }) {
    //     if (data) {
    //         this.options = data.childRelationships.map(relationship => ({ value: relationship.childObjectApiName, label: relationship.childObjectApiName }));
    //         console.log('this.options',JSON.stringify(this.options));

    //         this.RelatedObjectData = data;
    //         console.log('this.RelatedObjectData',JSON.stringify(this.RelatedObjectData));

    //         console.log('parentObjectOptions',JSON.stringify(data));
    //     } else if (error) {
    //         console.error('Error fetching object info:', error);
    //     }
    // }







    @track showData = [];
    @track showDuplicateRecords = false;
    @api objectApiName;

    @track recordName = '';
    @track recordEmail = '';
    
    columns = columns;

    //To Get current Record Name
    @api recordId;
    connectedCallback() {
        this.fetchRecordName();
    }

    async fetchRecordName() {
        try {
            const result = await getCurrentObjectRecordNameAndEmail({ recId: this.recordId }); 

            this.recordName = result['Name'];
                console.log('this.recordName ',this.recordName);
                this.recordEmail = result['Email__c'];
                console.log('this.recordEmail ',this.recordEmail);

            // this.recordName = result;
            console.log("Record Name: ", this.recordName);
        } catch (error) {
            console.error('Error fetching record name:', error);
        }
    }

     showButtonData() {
        this.showDuplicateRecords = true;
        getSObjectFieldsQuery({sObjectName: this.objectApiName,name:this.recordName, email:this.recordEmail, currentRecordId: this.recordId})
            .then(result => {
                console.log('result::::',result);
                // this.recordName = result.Name;
                this.showData = result;
                console.log('recordName::: ',this.showData?.Name);

            })
            .catch(error => {
                console.error('Error:', error);
            });
    }

      //Inline Edit
    // saveDraftValues = [];
    // handleSave(event) {
    //     this.saveDraftValues = event.detail.draftValues;
    //     const recordInputs = this.saveDraftValues.slice().map(draft => {
    //         const fields = Object.assign({}, draft);
    //         return { fields };
    //     });
 
    //     // Updateing the records using the UiRecordAPi
    //     const promises = recordInputs.map(recordInput => updateRecord(recordInput));
    //     Promise.all(promises).then(res => {
    //         this.ShowToast('Success', 'Records Updated Successfully!', 'success', 'dismissable');
    //         this.saveDraftValues = [];
    //         return this.refresh();
    //     }).catch(error => {
    //         this.ShowToast('Error', 'An Error Occured!!', 'error', 'dismissable');
    //     }).finally(() => {
    //         this.saveDraftValues = [];
    //     });
    // }
 
    // ShowToast(title, message, variant, mode){
    //     const evt = new ShowToastEvent({
    //             title: title,
    //             message:message,
    //             variant: variant,
    //             mode: mode
    //         });
    //         this.dispatchEvent(evt);
    // }

    //Get Selected Record Id
    @track getSelectedCheckBoxId;
    handleRowSelection(event){
        // alert('selected value:',event.detail.selectedRows)

        const selectedRows = event.detail.selectedRows;
        for(let i=0;i<selectedRows.length;i++){
            // alert('You select::: ',selectedRows[i].Id);
            console.log('ID::::::::::: ',selectedRows[i].Id)
            this.getSelectedCheckBoxId = selectedRows[i].Id;
            console.log('this.getSelectedCheckBoxId:: ',this.getSelectedCheckBoxId);
        }
    }

    
    // Merge Data
    @track showMergeData = false;
    async handleMergeData() {
        await Promise.all([
            this.getSObjectFields(),
            this.getCurrentRecord(),
            this.getSelectedRecord()
        ]);
        this.processData();
        this.showMergeData = true;
    }
    handleCancel(){
        this.showMergeData = false;
    }

    //Get Fields Name
    @track storeFieldNames;
    async getSObjectFields() {
        try {
            const result = await getSObjectFields({ sObjectName: this.objectApiName });
            console.log('Fields Name:', result);
            this.storeFieldNames = result;
        } catch (error) {
            console.error('Error:', error);
        }
    }

    // //Get Current Record Data
    @track storeCurrentRecData = [];
    @track storeFieldNamesss =[];
    async getCurrentRecord() {
        try {
            const result = await getCurrentRecord({ sObjectName: this.objectApiName, currentRecordId: this.recordId });
            console.log('Current Record:', result);
            this.storeCurrentRecData = Object.values(result[0]);
            this.storeFieldNamesss = Object.keys(result[0]);
            console.log('this.storeCurrentRecDatathis.storeCurrentRecData:: ',JSON.stringify(this.storeCurrentRecData));
            console.log('this.storeFieldNamesssthis.storeFieldNamesss:: ',JSON.stringify(this.storeFieldNamesss));
        } catch (error) {
            console.error('Error:', error);
        }
    }

    //Get Selected Checkbox Record
    @track storeSelectedRecData =[];
    @track dami;
    async getSelectedRecord() {
        try {
            const result = await getCurrentRecord({ sObjectName: this.objectApiName, currentRecordId: this.getSelectedCheckBoxId });
            console.log('Selected Record:', result);
            //Use Object.values to store only Values
            this.storeSelectedRecData = Object.values(result[0]);
            this.dami = Object.entries(result[0]).map(item=> item[1]);
            console.log('this.dami :: ',JSON.stringify(this.dami));
            console.log('this.storeSelectedRecData after result: ', JSON.stringify(this.storeSelectedRecData));

            // this.storeFieldNamesss = Object.keys(result[0]);

            // this.storeFieldNamesss = Object.keys(result[0]);

        } catch (error) {
            console.error('Error:', error);
        }
    }
    
    @track mergedData =[];
    // connectedCallback(){
    //     this.processData();
    // }
    processData() {
        console.log('this.storeFieldNames',JSON.stringify(this.storeFieldNamesss));
        console.log('this.storeCurrentRecData',JSON.stringify(this.storeCurrentRecData));
        console.log('this.storeSelectedRecData',JSON.stringify(this.storeSelectedRecData));

        const minLength  = Math.min(this.storeFieldNamesss?.length, this.storeCurrentRecData?.length, this.storeSelectedRecData?.length);
        console.log('minLength',minLength);
        for(let i=0;i<minLength;i++){
            console.log('inside loop ',i);
                const obj = {
                    field: this.storeFieldNamesss[i],
                    cr: this.storeCurrentRecData[i],
                    sr: this.storeSelectedRecData[i]
                };
                this.mergedData.push(obj);
            }
            console.log('this.mergedData::', JSON.stringify(this.mergedData));
        }
     
    
    @track selectedFields = [];
    getRadioBoxValue(event) {
        const radioBoxSelectedRecordValue = event.target.name;
        console.log('Selected Record Value: ', radioBoxSelectedRecordValue);
        if(event.target.checked){
            this.selectedFields.push(radioBoxSelectedRecordValue);
        }else{
            // Remove from selected fields if unchecked
            const index = this.selectedFields.indexOf(radioBoxSelectedRecordValue);
            console.log('indexx ',index);
            if(index !== -1){
                this.selectedFields.splice(index,1);
                console.log('selectedFields SPLICE ',this.selectedFields);
            }

        }
     }


    handleModalCancel(){
        this.showMergeData = false;
    }

        //To delete Merged Record
        deleteMergedRecord(mergeResult){
            console.log('button clicked delete');
            console.log('this.objectApiName deleted',JSON.stringify(this.objectApiName));
            console.log('this.mergeRecordResult deleted',mergeResult);
    
             return deleteMergedRecord({sObjectName: this.objectApiName, selectedRecordId: this.getSelectedCheckBoxId, mergeRecordResult: mergeResult})
             .then(result=>{
                console.log('deleted Succesfully:::', result);
             }).catch(error=>{
                console.log('Errororor on deleting',error);
             })
         }
    
    handleModalMerge(){
        this.handleReparenting();
        console.log('button clicked');
        console.log('selectedFields',JSON.stringify(this.selectedFields));
        console.log('this.objectApiName',JSON.stringify(this.objectApiName));
        console.log('this.getSelectedCheckBoxId',JSON.stringify(this.getSelectedCheckBoxId));
        console.log('this.recordId',JSON.stringify(this.recordId));

        return mergeRecord({sObjectName:this.objectApiName, selectedRecordId:this.getSelectedCheckBoxId, currentRecordId:this.recordId, selectedFields: this.selectedFields})
        .then(result=>{
            console.log('Merger result:: ',result);
            if(result == 'Merge Successfully'){
                const e = new ShowToastEvent({
                    title: 'Success!',
                    message: 'Record Merge Successfully!!!',
                    variant: 'success',
        });
            this.dispatchEvent(e);
            this.showMergeData = false;
            console.log('xxxxxxxxxxx::', result);
           // this.deleteMergedRecord();
         this.deleteMergedRecord(result);
        }

        }).catch(error=>{
            console.log(error);
        });
    }


    // for Reparenting
    // connectedCallback(){
    //     this.handleReparenting();
    // }

    handleReparenting(){
        console.log('---inside parenting---');
        console.log('parentObjectName:: ',this.objectApiName);
        console.log('parentRecordId ::: ',this.getSelectedCheckBoxId);
        console.log('current REcord Id ::: ',this.recordId);

        getAllChildRecordsAndUpdate({parentObjectName: this.objectApiName, parentRecordId :this.getSelectedCheckBoxId, CurrentRecordID: this.recordId})
        .then(result=>{
            console.log('child object with Fields::: ',result);
        }).catch(error=>{
            console.log('Error on parenting ' ,error);
        })
    }
}
```

Apex:-

```
public with sharing class customObjectDuplicateClass {
    
    //This method is used to return all accessible fields for an sObject
    @AuraEnabled
    public static List<String> getSObjectFields(String sObjectName) {
        // Initializing fieldNames set
        List<String> fieldNames = new List<String>();
        
        // Getting metadata of all sObjects
        Map<String, Schema.SObjectType> sObjectMap = Schema.getGlobalDescribe();
        
        // Getting the reference to current sObject
        Schema.SObjectType sObjectTypeInstance = sObjectMap.get(sObjectName);
        
        if(sObjectTypeInstance!=null) {
            
            // Getting Fields for current sObject
            Map<String, Schema.SObjectField> fieldMap = sObjectTypeInstance.getDescribe().fields.getMap();
            
            // Checking each field one by one, if it's accessible, adding it's name to fieldNames set
            for(Schema.SObjectField field: fieldMap.values()) {
                Schema.DescribeFieldResult fieldResult = field.getDescribe();
                if(fieldResult.isAccessible()) {
                    if(fieldResult.isUpdateable()){
                        fieldNames.add(fieldResult.getName());
                        
                    }
                }
            }
        }
        
        System.debug('Field Names::: '+ fieldNames);
        return fieldNames;        
    }
    
    // This method is used to return SOQL query consisting of all fields for an object that are accessible by the current user.
    @AuraEnabled
    public static List<SObject> getSObjectFieldsQuery(String sObjectName, String name, String email, Id currentRecordId) {
        
        // Getting field names
        List<String> fieldNames = getSObjectFields(sObjectName);
        
        String query = ' SELECT ';
        for(String fieldName : fieldNames) {
            query += ' ' + fieldName + ', ';
        }
        
        // Removing last 2 characters - ', '
        query = query.substring(0, query.lastIndexOf(','));
        query += ' FROM ' + sObjectName + ' WHERE Name = \'' + String.escapeSingleQuotes(name) + '\' AND Email__c = \'' + String.escapeSingleQuotes(email) + '\'';
        if(currentRecordId != null){
            query += 'AND Id != \''+ String.escapeSingleQuotes(currentRecordId) + '\'';
        }
        System.debug('query::: '+ query);
        List<SObject> records = Database.query(query);
        System.debug('records::: '+ records);
        
        return records;
    } 
    
    //To Get Current Record to show in Modal for Merge
    @AuraEnabled
    public static List<SObject> getCurrentRecord(String sObjectName, Id currentRecordId) {
        
        // Getting field names
        List<String> fieldNames = getSObjectFields(sObjectName);
        
        // Building query
        String query = ' SELECT ';
        for(String fieldName : fieldNames) {
            query += ' ' + fieldName + ', ';
        }
        
        // Removing last 2 characters - ', '
        query = query.substring(0, query.lastIndexOf(','));
        query += ' FROM ' + sObjectName + ' WHERE Id = \'' + String.escapeSingleQuotes(currentRecordId) + '\'';
        System.debug('query::: '+ query);
        List<SObject> records = Database.query(query);
        System.debug('recordsrecordsrecordsrecords : '+JSON.serialize(records));
        //to add Empty in Null Value
        
        for(SObject record: records){
            System.debug('inside SObject for '+record);
            for(String fieldName: fieldNames){
                System.debug('inside fieldName for '+fieldName);
                // Check if the field is editable
                Schema.DescribeFieldResult fieldDescribe = Schema.getGlobalDescribe().get(sObjectName).getDescribe().fields.getMap().get(fieldName).getDescribe();
                System.debug('fieldDescribeL ::: '+fieldDescribe);
                
                if(fieldDescribe.isUpdateable()){
                    Object value = record.get(fieldName);
                    if(value == null){
                        if(fieldDescribe.getType() == Schema.DisplayType.String){
                            System.debug('fieldDescribe.getType()'+fieldDescribe.getType());
                            System.debug('fieldNamefieldName:: '+fieldName);
                            record.put(fieldName, '-');
                        }else if(fieldDescribe.getType() == Schema.DisplayType.Double){
                            record.put(fieldName, 0.0); 
                        }
                    }
                }  
            }
        } 
        
        System.debug('records::: '+ JSON.serialize(records));
        //  String serialized =List<SObject> JSON.serialize(records);
        return records;  
    } 
    
    
    //To Get Current Record Name
    @AuraEnabled
    public static Map<String,String> getCurrentObjectRecordNameAndEmail(Id recId){
        Map<String,String> nameAndEmailInfo = new Map<String, String>();
        
        object objName = recId.getSobjectType();
        System.debug(objName);
        String query = 'Select Name,Email__c From '+objName+ ' WHERE Id=:recId LIMIT 1';
        Sobject myObj = Database.query(query);
        
        System.debug(String.valueOf(myObj.get('Name')));
        nameAndEmailInfo.put('Name',String.valueOf(myObj.get('Name')));
        nameAndEmailInfo.put('Email__c',String.valueOf(myObj.get('Email__c')));
        
        System.debug('Name:: '+ nameAndEmailInfo.get('Name'));
        System.debug('Email__c:: '+ nameAndEmailInfo.get('Email__c'));
        
        System.debug('nameAndEmailInfo::: '+nameAndEmailInfo);
        return nameAndEmailInfo;
    } 
    
    //To Merge the Records with Current Record
    //Current record sobt selected record le update krach ahe.
    @AuraEnabled
    public static String mergeRecord(String sObjectName, Id selectedRecordId,Id currentRecordId,List<String> selectedFields){
        // List<String> fieldNames = getSObjectFields(sObjectName); 
        
        List<SObject> currentRecordList = getCurrentRecord(sObjectName, currentRecordId);
        SObject currentRecord = currentRecordList[0];
        System.debug('currentRecord:: '+currentRecord);
        
        List<SObject> selectedRecordList = getCurrentRecord(sObjectName, selectedRecordId);
        SObject selectedRecord = selectedRecordList[0];
        System.debug('selectedRecord:: '+selectedRecord);
        
        List<String> fieldNames = new List<String>();
        for(String fieldName: selectedFields){
            System.debug('Inside for '+fieldName);
            //  if (selectedRecord.get(fieldName) != null) {
            //   System.debug('Inside If '+selectedRecord.get(fieldName));
            
            currentRecord.put(fieldName, selectedRecord.get(fieldName));
            // }
        }
        try{
            update currentRecord;
            System.debug('Updated Record '+ currentRecord);
            
        }catch(DmlException ex){
            System.debug('exxxx::: '+ex.getMessage());
            // return 'Updated Successfully!';
            
        }
        return 'Merge Successfully';
    }
    
    //To delete Merged Record
    @AuraEnabled
    public static String deleteMergedRecord(String sObjectName, String selectedRecordId, String mergeRecordResult){
        if(mergeRecordResult == 'Merge Successfully'){
            List<SObject> selectedRecordList = getCurrentRecord(sObjectName, selectedRecordId);
            SObject SelectedRecord = selectedRecordList[0];
            System.debug('SelectedRecord For delete:: '+ SelectedRecord);
            delete SelectedRecord;
        }
        return 'Deleted Successfully';
    }
    
    //To Get All Child Objects for reparenting
    public static Map<String, List<String>> getChildObjectsWithFields(String sObjectName){
        Map<string, List<String>> childObjectwithFields = new Map<String,List<String>>();
        
        Schema.DescribeSObjectResult describeResult = Schema.getGlobalDescribe().get(sObjectName).getDescribe();
        System.debug('describeResult '+ describeResult);
        System.debug('describeResult.getChildRelationships '+ describeResult.getChildRelationships());
        
        for(Schema.ChildRelationship cr:describeResult.getChildRelationships()){
            if(cr.getChildSObject().getDescribe().isUpdateable() && cr.getChildSObject().getDescribe().getKeyPrefix()!=null && !cr.getChildSObject().getDescribe().isCustomSetting() && cr.getChildSObject().getDescribe().isCreateable() && cr.getChildSObject().getDescribe().isAccessible()){
                String childObjectName = cr.getChildSObject().getDescribe().getName();
                
                List<String> childObjectFields = new List<String>();
                for(Schema.SObjectField field: cr.getChildSObject().getDescribe().fields.getMap().values()){
                    childObjectFields.add(field.getDescribe().getName());
                }
                
                childObjectwithFields.put(childObjectName, childObjectFields);
            }
        }
        System.debug('=====child object With Fields=====::: '+ childObjectwithFields);
        
        return childObjectwithFields;
    }
    
    
    //To Get Child Relationship Name
    public static String getChildRelationshipFieldName(String parentObjectName, String childObjectName) {
        String relationshipFieldName = '';
        // Describe calls to get child relationship
        Schema.DescribeSObjectResult parentDescribe = Schema.getGlobalDescribe().get(parentObjectName).getDescribe();
        Schema.DescribeSObjectResult childDescribe = Schema.getGlobalDescribe().get(childObjectName).getDescribe();
        // Iterate over parent fields to find the relationship field
        for (Schema.ChildRelationship relation : parentDescribe.getChildRelationships()) {
            System.debug('relation.getChildSObject().getDescribe().getName()::: '+relation.getChildSObject().getDescribe().getName());
            System.debug('childDescribe.getName::: '+childDescribe.getName());
            
            if (relation.getChildSObject().getDescribe().getName() == childDescribe.getName()) {
                System.debug('relation.getChildSObject().getDescribe().getName()::: '+relation.getChildSObject().getDescribe().getName());
                System.debug('childDescribe.getName::: '+childDescribe.getName());
                relationshipFieldName = relation.getField().getDescribe().getName();
                break;
            }
        }
        System.debug('relationshipFieldName :: '+relationshipFieldName);
        return relationshipFieldName;
    }
    
    
    //To Get All Child Record
    @AuraEnabled
    public static Map<String, List<SObject>> getAllChildRecordsAndUpdate (String parentObjectName,Id parentRecordId, Id CurrentRecordID){
        Map<String, List<SObject>> allChildRecords = new Map<String, List<SObject>>();
        Map<String, List<String>> getchildObjectWithField = getChildObjectsWithFields(parentObjectName);
        
        for(String childObjectName: getchildObjectWithField.keySet()){
            String relationshipFieldName = getChildRelationshipFieldName(parentObjectName, childObjectName);
            System.debug('relationshipFieldName:: '+relationshipFieldName);
            String query = 'SELECT ';
            List<String> fieldNames = getchildObjectWithField.get(childObjectName);  
            for(String fieldName: fieldNames){
                query += ' ' + fieldName + ', ';
            }
            
            query = query.substring(0, query.lastIndexOf(','));
            query += ' FROM ' + childObjectName + ' WHERE ' + relationshipFieldName + ' = \'' + String.escapeSingleQuotes(parentRecordId) + '\'';
            System.debug('query:::'+ query);
            List<SObject> childRecords = Database.query(query);
            System.debug('childRecords:: '+childRecords);
            if(childRecords.size()>0){
                allChildRecords.put(childObjectName, childRecords);
                System.debug('All Child Records:: '+ allChildRecords);
                for(SObject childRecord: childRecords){
                    childRecord.put(relationshipFieldName, currentRecordId);
                }
                try{
                    update childRecords;
                    System.debug('Updated Syy:: '+childRecords);
                }catch(Exception e){
                    System.debug('Error updating child records: ' + e.getMessage());
                }
            }
        }
        return allChildRecords;
    }
}

```
