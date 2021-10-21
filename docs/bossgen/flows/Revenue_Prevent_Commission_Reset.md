---
layout: default
title: Revenue_Prevent_Commission_Reset
parent: flows
---
# Metadata Type
flows


# Filename 
Revenue_Prevent_Commission_Reset


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Flow xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>50.0</apiVersion>
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
                <targetReference>myRule_1_pmetdec</targetReference>
            </connector>
            <label>Don&apos;t Allow 0 Commission</label>
        </rules>
    </decisions>
    <decisions>
        <name>myRule_1_pmetdec</name>
        <label>Previously Met Decision</label>
        <locationX>100</locationX>
        <locationY>100</locationY>
        <defaultConnector>
            <targetReference>myRule_1_A1</targetReference>
        </defaultConnector>
        <defaultConnectorLabel>Not Previously Met</defaultConnectorLabel>
        <rules>
            <name>myRule_1_pmetnullrule</name>
            <conditionLogic>or</conditionLogic>
            <conditions>
                <leftValueReference>myVariable_old</leftValueReference>
                <operator>IsNull</operator>
                <rightValue>
                    <booleanValue>true</booleanValue>
                </rightValue>
            </conditions>
            <connector>
                <targetReference>myRule_1_A1</targetReference>
            </connector>
            <label>Previously Met - Null</label>
        </rules>
        <rules>
            <name>myRule_1_pmetrule</name>
            <conditionLogic>and</conditionLogic>
            <conditions>
                <leftValueReference>formula_myRule_1_pmetrule</leftValueReference>
                <operator>EqualTo</operator>
                <rightValue>
                    <booleanValue>true</booleanValue>
                </rightValue>
            </conditions>
            <label>Previously Met - Prev</label>
        </rules>
    </decisions>
    <description>Prevents the commission from being reset</description>
    <formulas>
        <processMetadataValues>
            <name>originalFormula</name>
            <value>
                <stringValue>PRIORVALUE([Revenue__c].Commission_Percent__c)</stringValue>
            </value>
        </processMetadataValues>
        <name>formula_2_myRule_1_A1_2249463981</name>
        <dataType>Number</dataType>
        <expression>PRIORVALUE({!myVariable_current.Commission_Percent__c})</expression>
        <scale>18</scale>
    </formulas>
    <formulas>
        <processMetadataValues>
            <name>originalFormula</name>
            <value>
                <stringValue>AND(PRIORVALUE([Revenue__c].Commission_Percent__c ) &gt; 0, [Revenue__c].Commission_Percent__c = 0)</stringValue>
            </value>
        </processMetadataValues>
        <name>formula_myRule_1</name>
        <dataType>Boolean</dataType>
        <expression>AND(PRIORVALUE({!myVariable_current.Commission_Percent__c} ) &gt; 0, {!myVariable_current.Commission_Percent__c} = 0)</expression>
    </formulas>
    <formulas>
        <processMetadataValues>
            <name>originalFormula</name>
            <value>
                <stringValue>AND(PRIORVALUE([Revenue__c].Commission_Percent__c ) &gt; 0, [Revenue__c].Commission_Percent__c = 0)</stringValue>
            </value>
        </processMetadataValues>
        <name>formula_myRule_1_pmetrule</name>
        <dataType>Boolean</dataType>
        <expression>AND(PRIORVALUE({!myVariable_old.Commission_Percent__c} ) &gt; 0, {!myVariable_old.Commission_Percent__c} = 0)</expression>
    </formulas>
    <interviewLabel>Revenue_Prevent_Commission_Reset-1_InterviewLabel</interviewLabel>
    <label>Revenue: Prevent Commission Reset</label>
    <processMetadataValues>
        <name>ObjectType</name>
        <value>
            <stringValue>Revenue__c</stringValue>
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
            <stringValue>onAllChanges</stringValue>
        </value>
    </processMetadataValues>
    <processType>Workflow</processType>
    <recordUpdates>
        <processMetadataValues>
            <name>evaluationType</name>
            <value>
                <stringValue>always</stringValue>
            </value>
        </processMetadataValues>
        <processMetadataValues>
            <name>extraTypeInfo</name>
        </processMetadataValues>
        <processMetadataValues>
            <name>isChildRelationship</name>
            <value>
                <booleanValue>false</booleanValue>
            </value>
        </processMetadataValues>
        <processMetadataValues>
            <name>reference</name>
            <value>
                <stringValue>[Revenue__c]</stringValue>
            </value>
        </processMetadataValues>
        <processMetadataValues>
            <name>referenceTargetField</name>
        </processMetadataValues>
        <name>myRule_1_A1</name>
        <label>Put Old Commission Back</label>
        <locationX>100</locationX>
        <locationY>200</locationY>
        <filterLogic>and</filterLogic>
        <filters>
            <processMetadataValues>
                <name>implicit</name>
                <value>
                    <booleanValue>true</booleanValue>
                </value>
            </processMetadataValues>
            <field>Id</field>
            <operator>EqualTo</operator>
            <value>
                <elementReference>myVariable_current.Id</elementReference>
            </value>
        </filters>
        <inputAssignments>
            <processMetadataValues>
                <name>dataType</name>
                <value>
                    <stringValue>Number</stringValue>
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
                    <stringValue>Commission %</stringValue>
                </value>
            </processMetadataValues>
            <processMetadataValues>
                <name>leftHandSideReferenceTo</name>
                <value>
                    <stringValue/>
                </value>
            </processMetadataValues>
            <processMetadataValues>
                <name>rightHandSideType</name>
                <value>
                    <stringValue>Formula</stringValue>
                </value>
            </processMetadataValues>
            <field>Commission_Percent__c</field>
            <value>
                <elementReference>formula_2_myRule_1_A1_2249463981</elementReference>
            </value>
        </inputAssignments>
        <object>Revenue__c</object>
    </recordUpdates>
    <startElementReference>myDecision</startElementReference>
    <status>Active</status>
    <variables>
        <name>myVariable_current</name>
        <dataType>SObject</dataType>
        <isCollection>false</isCollection>
        <isInput>true</isInput>
        <isOutput>true</isOutput>
        <objectType>Revenue__c</objectType>
    </variables>
    <variables>
        <name>myVariable_old</name>
        <dataType>SObject</dataType>
        <isCollection>false</isCollection>
        <isInput>true</isInput>
        <isOutput>false</isOutput>
        <objectType>Revenue__c</objectType>
    </variables>
</Flow>
```


# Last Modified


# Usage
