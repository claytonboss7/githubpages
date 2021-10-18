---
layout: default
title: ReportPickListValues
parent: classes
---

```global class ReportPickListValues extends VisualEditor.DynamicPickList{
    
    global override VisualEditor.DataRow getDefaultValue(){
        VisualEditor.DataRow defaultValue = new VisualEditor.DataRow('select report','select report');
        return defaultValue;
    }
    global override VisualEditor.DynamicPickListRows getValues() {

        Report[] theReports = [SELECT Name From Report];

        VisualEditor.DynamicPickListRows myValues = new VisualEditor.DynamicPickListRows();
        VisualEditor.DataRow defValue = new VisualEditor.DataRow('select report','select report');
        myValues.addRow(defValue);
        for(Report rep : theReports){

            VisualEditor.DataRow p1 = new VisualEditor.DataRow(rep.Name, String.valueOf(rep.Id));
            myValues.addRow(p1);
            system.debug(p1);
        }
        return myValues;
    }

}```
