# best-repo-ever hItesh reddy first git repoimport { LightningElement, wire, track,api } from 'lwc';
import { NavigationMixin } from 'lightning/navigation';
import { ShowToastEvent } from 'lightning/platformShowToastEvent';
import { getRecord ,getRecordNotifyChange} from 'lightning/uiRecordApi';
import getUserDetails from '@salesforce/apex/CaseReassign_Escalation.getUserDetails';
import CASE_OBJECT_REASON from '@salesforce/schema/Case.Reason__c';
import bwcCreateInteractionRecord from '@salesforce/apex/bwcCreateInteractionHelperClass.bwcCreateInteractionRecord';

export default class BwcCreateInteraction extends LightningElement {
    @api recordId;
    @track selSearchReason = "";
    @track seluserId='';
    @track searchReasons = [];
    //@track selectOptUsers = [{label: "--None--", value: ""}];
    @track isShowAll = false;
    @track fieldValue;
    @api showReasonField = false;
    @track searchValue = '';
    @track value= 'Testing';


    get options(){
        return [
            { label: 'New', value: 'new' },
            { label: 'In Progress', value: 'inProgress' },
            { label: 'Finished', value: 'finished' },
        ];

    }

    connectedCallback() {
        console.log("###connectedCallback");
    }

    handleSearchCustomer(){
        console.log("###interaction created");
        this.showReasonField = true;
        //this.searchValue = 'Reason';
        const searchValue = true;

        var valueChangeEvent = new CustomEvent('valuechange', {detail: { value: this.searchValue }
          });
          // Fire the custom event
          this.dispatchEvent(valueChangeEvent);
        
    }

    cancelClicked(){
        console.log("clicked Cancel");
        this.showReasonField = false;
        this.value = '--None--';
    }

    handleChange(event){
        console.log('Entered Value');
        this.value = event.detail.value;
      
    }

    handleProceedtoSearch(event){


        bwcCreateInteractionRecord({ accountId : this.recordId}).then(result => {
            
            console.log("final New");
            
        })
        .catch(error => {
            this.dispatchEvent(new ShowToastEvent({
                title: 'Error!!',
                message: errorPhase.body.message,
                variant: 'error'
            }));

        });
        this.showReasonField= false;


    }
}
