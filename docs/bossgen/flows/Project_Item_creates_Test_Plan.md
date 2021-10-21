---
layout: default
title: Project_Item_creates_Test_Plan
parent: flows
---
# Metadata Type
flows


# Filename 
Project_Item_creates_Test_Plan


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Flow xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <decisions>
        <processMetadataValues>
            <name>index</name>
            <value>
                <numberValue>0.0</numberValue>
            </value>
        </processMetadataValues>
        <name>myDecision</name>
        <label>myDecision</label>
        <locationX>50</locationX>
        <locationY>0</locationY>
        <defaultConnectorLabel>default</defaultConnectorLabel>
        <rules>
            <name>myRule_1</name>
            <conditionLogic>and</conditionLogic>
            <conditions>
                <leftValueReference>formula_myRule_1</leftValueReference>
                <operator>EqualTo</operator>
                <rightValue>
                    <booleanValue>true</booleanValue>
                </rightValue>
            </conditions>
            <connector>
                <targetReference>myRule_1_A1</targetReference>
            </connector>
            <label>Record Created</label>
        </rules>
    </decisions>
    <description>This should create a test plan for every new Story in PT</description>
    <formulas>
        <processMetadataValues>
            <name>originalFormula</name>
            <value>
                <stringValue>&quot;QA - &quot; &amp; [Project_Item__c].Story_Id__c &amp; &quot;  -  &quot;  &amp; [Project_Item__c].Story_Name__c</stringValue>
            </value>
        </processMetadataValues>
        <name>formula_2_myRule_1_A1_2354898885</name>
        <dataType>String</dataType>
        <expression>&quot;QA - &quot; &amp; {!myVariable_current.Story_Id__c} &amp; &quot;  -  &quot;  &amp; {!myVariable_current.Story_Name__c}</expression>
    </formulas>
    <formulas>
        <name>formula_myRule_1</name>
        <dataType>Boolean</dataType>
        <expression>true</expression>
    </formulas>
    <interviewLabel>Project_Item_creates_Test_Plan-1_InterviewLabel</interviewLabel>
    <label>Project Item creates Test Plan</label>
    <processMetadataValues>
        <name>ObjectType</name>
        <value>
            <stringValue>Project_Item__c</stringValue>
        </value>
    </processMetadataValues>
    <processMetadataValues>
        <name>ObjectVariable</name>
        <value>
            <elementReference>myVariable_current</elementReference>
        </value>
    </processMetadataValues>
    <processMetadataValues>
        <name>OldObjectVariable</name>
        <value>
            <elementReference>myVariable_old</elementReference>
        </value>
    </processMetadataValues>
    <processMetadataValues>
        <name>TriggerType</name>
        <value>
            <stringValue>onCreateOnly</stringValue>
        </value>
    </processMetadataValues>
    <processType>Workflow</processType>
    <recordCreates>
        <name>myRule_1_A1</name>
        <label>Create Test Plan</label>
        <locationX>100</locationX>
        <locationY>200</locationY>
        <inputAssignments>
            <processMetadataValues>
                <name>dataType</name>
                <value>
                    <stringValue>String</stringValue>
                </value>
            </processMetadataValues>
            <processMetadataValues>
                <name>isRequired</name>
                <value>
                    <booleanValue>false</booleanValue>
                </value>
            </processMetadataValues>
            <processMetadataValues>
                <name>leftHandSideLabel</name>
                <value>
                    <stringValue>Test Plan Name</stringValue>
                </value>
            </processMetadataValues>
            <processMetadataValues>
                <name>rightHandSideType</name>
                <value>
                    <stringValue>Formula</stringValue>
                </value>
            </processMetadataValues>
            <field>Name</field>
            <value>
                <elementReference>formula_2_myRule_1_A1_2354898885</elementReference>
            </value>
        </inputAssignments>
        <object>Test_Plan__c</object>
    </recordCreates>
    <startElementReference>myDecision</startElementReference>
    <status>Active</status>
    <variables>
        <name>myVariable_current</name>
        <dataType>SObject</dataType>
        <isCollection>false</isCollection>
        <isInput>true</isInput>
        <isOutput>true</isOutput>
        <objectType>Project_Item__c</objectType>
    </variables>
    <variables>
        <name>myVariable_old</name>
        <dataType>SObject</dataType>
        <isCollection>false</isCollection>
        <isInput>true</isInput>
        <isOutput>false</isOutput>
        <objectType>Project_Item__c</objectType>
    </variables>
</Flow>
```


# Last Modified


# Usage
