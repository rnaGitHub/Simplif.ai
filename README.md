Introduction
    Project Name: 
        Automated Custom Document Model Processor test

    Synopsis: 
        This project aims to build an automated custom document processing pipeline. The specifix use case in this project is to load and analyze Patient Discharge Summary documents. 
    
        The solution uses Azure Form Recognizer for the structured extraction of data and Natural language processing (NLP) models to enrich the extracted data. Specifically, Text Analytics for health libraries have been used to extract and label relevant medical information. 
        
        This includes Named Entity Recognition features to detect words and phrases mentioned in unstructured text (e.g. Doctor's Notes) that can be associated with one or more semantic types, such as diagnosis, medication name, symptom/sign, or age. Relation extraction features identifies meaningful connections between concepts mentioned in text. For example, a "time of condition" relation is found by associating a condition name with a time or between an abbreviation and the full description. 
        
        Another important feature is Entity linking to concepts found in a predefined database of concepts including the Unified Medical Language System (UMLS).  

    Process Flow: 

Prerequisites
    Python 3.7 or later is required to use this package
    You must have an Azure subscription and an Azure Form Recognizer account to run these samples.


Requirements
    Install the Azure Form Recognizer client library for Python with pip:
        pip install azure-ai-formrecognizer

    Install the Azure Text Analytics for Health client library for Python with pip:
        pip install azure-ai-textanalytics==5.2.0

    Clone or download this sample repository

    Open the sample folder in Visual Studio Code or your IDE of choice.
        Directory Structure:
        Capstone
            - .env
            - test_model
                - sample_forms


Setup
    Open a terminal window and cd to the directory that the samples are saved in. 
        - cd Capstone\test_model\sample_forms
    Review the test files. There should be 4 files in the folder.
        - Patient_Discharge_Summary_6.pdf
        - Patient_Discharge_Summary_7.pdf
        - Patient_Discharge_Summary_8.pdf
        - Patient_Discharge_Summary_9.pdf
    Review the environment variables in the .env file in the root directory. 
        - It contains the endpoint and keys for the Form Recogizer service and Language service and the Azure Storage container. In a production scenario, these keys need to be securely kept in key vault or secrets file.
    Cd to the scripts directory 
        - cd Capstone\test_model
    Run the python script 
        - python Document_Processor.py Patient_Discharge_Summary_6.pdf
        Repeat the same for the other 3 files by passing the respective filename as argument to the command above.



OUTPUT:

    PS C:\Users\ramanna\OneDrive - Insight\Desktop\Simplif.AI\Capstone\test_model> python Document_Processor.py Patient_Discharge_Summary_8.pdf

    Grace Clinic

    New Ballas Rd Saint Louis, MO 63141

    ___________________________________________________________________________________________________________________________________________

                                                Patient Discharge Summary
                                                _________________________

    Patient Information:
        Phone: 373 134 6655
        DOB: 08/10/1962
        Member_Id: 10008
        City_St_Zip: Pasadena CA 91533
        Provider: Providence Healthcare
        Address: 12 Dryden Street
        Patient_Name: Dean Jones
        Allergy: None

    Prescription Information:
        Drug_Name: Percocet       Strength: Tablet: 500 mg.       Directions: Take once a day       Quantity: 30       Refills: 0
        Drug_Name: Tramadol       Strength: Tablet: 100 mg.       Directions: Take once a day       Quantity: 30       Refills: 0

    Doctors Notes:
        Patient is a 60 year old male and was admitted for a right total Hip Arthroplasty following a fall in his home. Patient was taken to the OR and underwent the above procedure and was taken to the PACU in stable condition. The wound was healing without evidence of infection. He received Cefuroxime via IV. All doses were given within 24 hours of surgery. At the time of discharge the pain was well controlled on oral Analgesics. At the time of discharge, physical therapy was started on POD#1 that needs to be continued at home. In case of continued pain, the patient can take 100 mg of Tramadol and 500 mg of Percocet for severe pain,

    Doctors Notes (using Text Analytics for health features):
        Patient is a 60 year old male [Gender] [C0025266 - UMLS] and was admitted [AdministrativeEvent] for a right [Direction] total Hip Arthroplasty following a fall [SymptomOrSign] [C0085639 - UMLS] in his home. Patient was taken to the OR [CareEnvironment] and underwent the above procedure and was taken to the PACU [CareEnvironment] in stable condition. The wound [SymptomOrSign] [C0043250 - UMLS] was healing [Course] without evidence of infection. He received Cefuroxime [MedicationName] [C0007562 - UMLS] via IV. All doses were given within [RelationalOperator] 24 hours of surgery. At the time of discharge [AdministrativeEvent] [AdministrativeEvent] the pain [SymptomOrSign] [C0030193 - UMLS] [SymptomOrSign] [C0030193 - UMLS] [SymptomOrSign] [C0030193 - UMLS] was well controlled on oral [MedicationRoute] Analgesics. At the time of discharge, physical therapy was started on POD#1 [Time] that needs to be continued [Course] [Course] at home. In case of continued [Course] [Course] pain, the patient can take 100 mg of Tramadol [MedicationName] [C0040610 - UMLS] and 500 mg of Percocet [MedicationName] [C0086787 - UMLS] for severe [ConditionQualifier] pain,

        Medication: Tramadol, Dosage: 600 mg
        Wikipedia link: https://en.wikipedia.org/wiki/Tramadol
    ___________________________________________________________________________________________________________________________________________     
