---
layout: default
title: Dashboard_Dialog_Documents
parent: classes
---

```public class Dashboard_Dialog_Documents {
	public String relativeRecordId { get; set; }
	public String relativeParentSObjectName { get; set; }
	public String relativeParentId { get; set; }
	public String opportunityId { get; set; }
	public Boolean isBidContract { get; set; }
	public String housingRT { get; set; }
	public String documentListJSON { get; set; }
	public String documentUploadAction { get; set; }
	public String linkId { get; set; }
	public String shareId { get; set; }
	public String fileId { get; set; }
	public String fileName { get; set; }
	public String fileType { get; set; }
	public String fileBody { get; set; }
	public String fileInsertedJSON { get; set; }
	public Boolean isShared { get; set; }
	public String emailJSON { get; set; }
	public String emailMessage { get; set; }
	public List<DocumentWrapper> documents { get; set; }
	public List<ContentDocument> documentList { get; set; }
	public List<ButtonWrapper> documentButtons { get; set; }

	/**
	 * getDocuments description
	 */
	public void getDocuments() {
		if (String.isBlank(fileInsertedJSON))
			fileInsertedJSON = '{}';
		if (String.isBlank(emailMessage))
			emailMessage = '';
		documents = new List<DocumentWrapper>();
		documentUploadAction = '';
		documentList = new List<ContentDocument>();
		documentListJSON = '[]';
		if (String.isNotBlank(relativeRecordId)) {
			Integer index = 0;
			Map<Id, Integer> documentsMap = new Map<Id, Integer>();
			System.debug(relativeParentId);
			if (relativeParentSObjectName.equals('Air')) {
				for (ContentDocumentLink cdl : [
					SELECT Id, LinkedEntityId, ContentDocumentId
					FROM ContentDocumentLink
					WHERE LinkedEntityId = :relativeParentId
				]) {
					documents.add(new DocumentWrapper(cdl.Id, cdl.ContentDocumentId));
					documentsMap.put(cdl.ContentDocumentId, index);
					index++;
				}
			} else {
				for (ContentDocumentLink cdl : [
					SELECT Id, LinkedEntityId, ContentDocumentId
					FROM ContentDocumentLink
					WHERE LinkedEntityId = :relativeRecordId
				]) {
					documents.add(new DocumentWrapper(cdl.Id, cdl.ContentDocumentId));
					documentsMap.put(cdl.ContentDocumentId, index);
					index++;
				}
			}
			System.debug('documentsMap size: ' + documentsMap.size());
			for (ContentDocument document : [
				SELECT Id, Title, FileExtension, CreatedDate, ContentSize, LatestPublishedVersionId, Owner.ContactId
				FROM ContentDocument
				WHERE Id IN :documentsMap.keySet()
				ORDER BY CreatedDate DESC
			]) {
				documents.get(documentsMap.get(document.Id)).versionId = document.LatestPublishedVersionId;
				documents.get(documentsMap.get(document.Id)).title = document.Title.replaceAll('\'', '');
				documents.get(documentsMap.get(document.Id)).extension = document.FileExtension;
				documents.get(documentsMap.get(document.Id)).createdDate = document.CreatedDate;
				documents.get(documentsMap.get(document.Id)).contentSize = document.ContentSize;
				documents.get(documentsMap.get(document.Id)).isFromCommunity = String.isNotBlank(document.Owner.ContactId) ? true : false;
				documentList.add(document);
			}
			Set<String> documentListIds = new Set<String>();
			for (ContentDocument cd : documentList)
				documentListIds.add(cd.Id);
			for (Share__c share : [SELECT Id, WhatID__c, isForCustomers__c, isForVendors__c FROM Share__c WHERE WhatID__c IN :documentListIds]) {
				documents.get(documentsMap.get(share.WhatID__c)).shareId = share.Id;
				documents.get(documentsMap.get(share.WhatID__c)).isForCustomers = share.isForCustomers__c;
				documents.get(documentsMap.get(share.WhatID__c)).isForVendors = share.isForVendors__c;
			}
			System.debug('# of documents: ' + documents.size());
			documentListJSON = JSON.serialize(documents);
		}
		documentButtons = new List<ButtonWrapper>();
		documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Upload', 'OpenFileSelector(\'normal\');', 'normal'));
		if (isBidContract) {
			switch on relativeParentSObjectName {
				when 'Housing' {
					housingRT = '';
					List<Bid__c> searchBid = [SELECT Housing_Record_Type__c FROM Bid__c WHERE Id = :relativeRecordId LIMIT 1];
					if (!searchBid.isEmpty()) {
						housingRT = searchBid.get(0).Housing_Record_Type__c;
						switch on housingRT {
							when 'Hotel Housing' {
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Contract', 'OpenFileSelector(\'Contract\');', 'Contract')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper(
										'Contract to Client',
										'OpenFileSelector(\'ContractToClient\');',
										'ContractToClient'
									)
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Final Contract', 'OpenFileSelector(\'Final\');', 'Final')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Date Change', 'OpenFileSelector(\'DateChange\');', 'DateChange')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('No Rooms PU', 'OpenFileSelector(\'NoRoomsPU\');', 'NoRoomsPU')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Cancellation', 'OpenFileSelector(\'Cancellation\');', 'Cancellation')
								);
								documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('GCIP', 'OpenFileSelector(\'GCIP\');', 'GCIP'));
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Rooming List', 'OpenFileSelector(\'RoomingList\');', 'RoomingList')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper(
										'Contract Client Signed',
										'OpenFileSelector(\'ContractClientSigned\');',
										'ContractClientSigned'
									)
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Booking Link', 'OpenFileSelector(\'BookingLink\');', 'BookingLink')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper(
										'Hotel Confirmations',
										'OpenFileSelector(\'HotelConfirmations\');',
										'HotelConfirmations'
									)
								);
							}
							when 'Corporate Housing' {
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Rate Agreement', 'OpenFileSelector(\'RateAgreement\');', 'RateAgreement')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Date Change', 'OpenFileSelector(\'DateChange\');', 'DateChange')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Cancellation', 'OpenFileSelector(\'Cancellation\');', 'Cancellation')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Rooming List', 'OpenFileSelector(\'RoomingList\');', 'RoomingList')
								);
							}
							when 'Individual Reservation' {
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Rate Agreement', 'OpenFileSelector(\'RateAgreement\');', 'RateAgreement')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper('Signed CC Auth', 'OpenFileSelector(\'SignedCCAuth\');', 'SignedCCAuth')
								);
								documentButtons.add(
									new Dashboard_Dialog_Documents.ButtonWrapper(
										'Confirmation Numbers',
										'OpenFileSelector(\'ConfirmationNumbers\');',
										'ConfirmationNumbers'
									)
								);
							}
						}
						documentButtons.add(
							new Dashboard_Dialog_Documents.ButtonWrapper('Pick Up Report', 'OpenFileSelector(\'PickUpReport\');', 'PickUpReport')
						);
					}
				}
				when 'Ground' {
					documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Contract', 'OpenFileSelector(\'Contract\');', 'Contract'));
					documentButtons.add(
						new Dashboard_Dialog_Documents.ButtonWrapper(
							'Contract to Client',
							'OpenFileSelector(\'ContractToClient\');',
							'ContractToClient'
						)
					);
					documentButtons.add(
						new Dashboard_Dialog_Documents.ButtonWrapper(
							'Contract Client Signed',
							'OpenFileSelector(\'ContractClientSigned\');',
							'ContractClientSigned'
						)
					);
					documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Final', 'OpenFileSelector(\'Final\');', 'Final'));
					documentButtons.add(
						new Dashboard_Dialog_Documents.ButtonWrapper('Trip Update', 'OpenFileSelector(\'TripUpdate\');', 'TripUpdate')
					);
					documentButtons.add(
						new Dashboard_Dialog_Documents.ButtonWrapper('Cancellation', 'OpenFileSelector(\'Cancellation\');', 'Cancellation')
					);
				}
				when 'Air' {
					List<Bid__c> bids = [SELECT id, Air_Charter__c FROM Bid__c WHERE Id = :relativeRecordId LIMIT 1];
					if (!bids.isEmpty() && !bids[0].Air_Charter__c) {
						documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Name List', 'OpenFileSelector(\'NameList\');', 'NameList'));
						documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Contract', 'OpenFileSelector(\'Contract\');', 'Contract'));
						documentButtons.add(
							new Dashboard_Dialog_Documents.ButtonWrapper(
								'Deposit/LOCSignedContract',
								'OpenFileSelector(\'DepositLOCSignedContract\');',
								'DepositLOCSignedContract'
							)
						);
					}
				}
			}
		}
		documentButtons.add(new Dashboard_Dialog_Documents.ButtonWrapper('Send Mail', 'OpenEmailModal();', 'none'));
	}

	public void UploadDocument() {
		fileInsertedJSON = '{}';
		system.debug(documentUploadAction);
		system.debug(fileName);
		system.debug(fileBody);
		if (String.isNotBlank(documentUploadAction) && String.isNotBlank(fileName) && String.isNotBlank(fileBody)) {
			try {
				Id bidParentId = null;
				ContentVersion contentVersion = new ContentVersion();
				contentVersion.PathOnClient = '/' + fileName;
				contentVersion.VersionData = (fileBody.length() > 100
					? EncodingUtil.base64Decode(fileBody.subString(0, 100).split(',')[1] + fileBody.substring(100, fileBody.length()))
					: EncodingUtil.base64Decode(fileBody.split(',')[1]));
				Decimal correlative = null;
				Bid__c bidContracted = new Bid__c();
				List<Task> traceTasks = new List<Task>();
				String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId();
				if (isBidContract) {
					Datetime startDate = Datetime.now();
					List<Bid__c> searchBid = new List<Bid__c>();
					switch on relativeParentSObjectName {
						when 'Housing' {
							searchBid = [
								SELECT
									Contract_first_only__c,
									Vendor__c,
									Vendor__r.Name,
									Housing__c,
                                	Final_Status__c,
									Housing__r.City__c,
									Housing__r.City__r.Name,
									Housing__r.City__r.State__c,
									Housing__r.Date_Out__c,
									Housing__r.Date_In__c,
									isFromTournament__c,
									Housing__r.Tournament__c
								FROM Bid__c
								WHERE Id = :relativeRecordId
								LIMIT 1
							];
							if (!searchBid.isEmpty()) {
								bidParentId = searchBid.get(0).Housing__c;
								if (searchBid.get(0).Housing__r.Date_In__c != null)
									startDate = Datetime.newInstance(searchBid.get(0).Housing__r.Date_In__c, Time.newInstance(0, 0, 0, 0));
							}
						}
						when 'Ground' {
							searchBid = [
								SELECT Contract_first_only__c, Vendor__c, Vendor__r.Name, GT__c, GT__r.Start_Date__c, GT_Description__c
								FROM Bid__c
								WHERE Id = :relativeRecordId
								LIMIT 1
							];
							if (!searchBid.isEmpty()) {
								bidParentId = searchBid.get(0).GT__c;
								if (searchBid.get(0).GT__r.Start_Date__c != null)
									startDate = Datetime.newInstance(searchBid.get(0).GT__r.Start_Date__c, Time.newInstance(0, 0, 0, 0));
							}
						}
						when 'Air' {
							searchBid = [
								SELECT
									Contract_first_only__c,
									Vendor__c,
									Vendor__r.Name,
									Air__c,
									Air__r.Departure_Date__c,
									Air__r.Description__c,
									Air__r.Group_Type__c
								FROM Bid__c
								WHERE Id = :relativeRecordId
								LIMIT 1
							];
							if (!searchBid.isEmpty()) {
								bidParentId = searchBid.get(0).Air__c;
								if (searchBid.get(0).Air__r.Departure_Date__c != null)
									startDate = Datetime.newInstance(searchBid.get(0).Air__r.Departure_Date__c, Time.newInstance(0, 0, 0, 0));
							}
						}
					}
					if (!searchBid.isEmpty())
						bidContracted = searchBid.get(0);
					system.debug('searchBid :: ' + searchBid);
					if (bidContracted.Id != null) {
						String vendorName = String.isNotEmpty(bidContracted.Vendor__c) ? '-' + bidContracted.Vendor__r.Name : '';
						if (documentUploadAction.equals('normal'))
							contentVersion.Title = fileName.split('\.')[0];
						else
							switch on relativeParentSObjectName {
								when 'Housing' {
									String cityName = String.isNotEmpty(bidContracted.Housing__r.City__c) ? '-' + bidContracted.Housing__r.City__r.Name : '';
									String stateName = String.isNotEmpty(bidContracted.Housing__r.City__c)
										? '-' + bidContracted.Housing__r.City__r.State__c
										: '';
									String todayDate = '-' + startDate.format('dd-MMM-yyyy');
									if (!documentUploadAction.equals('normal')) {
										contentVersion.Title = documentUploadAction;
										correlative = 0;
										for (ContentDocument findFinal : documentList)
											if (
												findFinal.Title.length() > contentVersion.Title.length() &&
												findFinal.Title.substring(0, contentVersion.Title.length()).equals(contentVersion.Title)
											)
												correlative = 1;
										for (ContentDocument findFinal : documentList)
											if (findFinal.Title.substringBetween(contentVersion.Title + '_', '-') != null) {
												if (
													findFinal.Title.substringBetween(contentVersion.Title + '_', '-').isNumeric() &&
													Integer.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-')) >= correlative.intValue()
												)
													correlative = Decimal.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-'));
											}
										if (correlative > 0)
											contentVersion.Title += '_' + (correlative.intValue() + 1);
										contentVersion.Title += vendorName + cityName + stateName;
										contentVersion.Title = contentVersion.Title.replaceAll('\s+', '');
										if (contentVersion.Title.length() > 90)
											contentVersion.Title = contentVersion.Title.substring(0, 90);
									} else
										contentVersion.Title = fileName.split('\.')[0];
									contentVersion.Title += todayDate;
								}
								when 'Ground' {
									String description = String.isNotEmpty(bidContracted.GT_Description__c) ? '-' + bidContracted.GT_Description__c : '';
									String todayDate = '-' + startDate.format('dd-MMM-yyyy');
									if (
										documentUploadAction.equals('Contract') ||
										documentUploadAction.equals('ContractToClient') ||
										documentUploadAction.equals('ContractClientSigned')
									)
										contentVersion.Title = 'Transportation';
									contentVersion.Title += documentUploadAction;
									correlative = 0;
									for (ContentDocument findFinal : documentList)
										if (
											findFinal.Title.length() > contentVersion.Title.length() &&
											findFinal.Title.substring(0, contentVersion.Title.length()).equals(contentVersion.Title)
										)
											correlative = 1;
									for (ContentDocument findFinal : documentList)
										if (findFinal.Title.substringBetween(contentVersion.Title + '_', '-') != null) {
											if (
												findFinal.Title.substringBetween(contentVersion.Title + '_', '-').isNumeric() &&
												Integer.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-')) >= correlative.intValue()
											)
												correlative = Decimal.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-'));
										}
									if (correlative > 0)
										contentVersion.Title += '_' + (correlative.intValue() + 1);
									contentVersion.Title += vendorName + description;
									contentVersion.Title = contentVersion.Title.replaceAll('\s+', '');
									if (contentVersion.Title.length() > 90)
										contentVersion.Title = contentVersion.Title.substring(0, 90);
									contentVersion.Title += todayDate;
								}
								when 'Air' {
									String todayDate = '-' + startDate.format('dd-MMM-yy');
									contentVersion.Title = documentUploadAction;
									correlative = 0;
									for (ContentDocument findFinal : documentList)
										if (
											findFinal.Title.length() > contentVersion.Title.length() &&
											findFinal.Title.substring(0, contentVersion.Title.length()).equals(contentVersion.Title)
										)
											correlative = 1;
									for (ContentDocument findFinal : documentList)
										if (findFinal.Title.substringBetween(contentVersion.Title + '_', '-') != null) {
											if (
												findFinal.Title.substringBetween(contentVersion.Title + '_', '-').isNumeric() &&
												Integer.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-')) >= correlative.intValue()
											)
												correlative = Decimal.valueOf(findFinal.Title.substringBetween(contentVersion.Title + '_', '-'));
										}
									if (correlative > 0)
										contentVersion.Title += '_' + (correlative.intValue() + 1);
									contentVersion.Title += vendorName;
									contentVersion.Title = contentVersion.Title.replaceAll('\s+', '');
									if (contentVersion.Title.length() > 90)
										contentVersion.Title = contentVersion.Title.substring(0, 90);
									contentVersion.Title += todayDate;
								}
								when else {
									contentVersion.Title = fileName.split('\.')[0];
								}
							}
					} else
						contentVersion.Title = fileName.split('\.')[0];
				} else
					contentVersion.Title = fileName.split('\.')[0];

				Pattern nonAlphanumeric = Pattern.compile('[^a-zA-Z0-9]');
				Matcher matcher = nonAlphanumeric.matcher('Sales - Actual Results (TY)');

				insert contentVersion;
				ContentVersion contentVersionInserted = [
					SELECT ContentDocumentId, ContentDocument.FileExtension
					FROM ContentVersion
					WHERE Id = :contentVersion.Id
				];
				//Create ContentDocumentLink
				ContentDocumentLink contentDocumentLink = new ContentDocumentLink();
				contentDocumentLink.ContentDocumentId = contentVersionInserted.ContentDocumentId;
				if (relativeParentSObjectName.equals('Air')) {
					List<Bid__c> searchBid = [SELECT Id, Air__c FROM Bid__c WHERE Id = :relativeRecordId LIMIT 1];
					if (!searchBid.isEmpty())
						contentDocumentLink.LinkedEntityId = searchBid.get(0).Air__c;
				} else
					contentDocumentLink.LinkedEntityId = relativeRecordId;
				contentDocumentLink.ShareType = 'V';
				contentDocumentLink.Visibility = 'AllUsers';
				insert contentDocumentLink;
				if (bidParentId != null) {
					contentDocumentLink.Id = null;
					contentDocumentLink.LinkedEntityId = bidParentId;
					insert contentDocumentLink;
				}

				List<ContentDocument> findFileInserted = [
					SELECT Id, Title, FileExtension, CreatedDate, ContentSize
					FROM ContentDocument
					WHERE Id = :contentVersionInserted.ContentDocumentId
					LIMIT 1
				];
				if (!findFileInserted.isEmpty())
					fileInsertedJSON = JSON.serialize(findFileInserted.get(0));

				if (bidContracted.Id != null) {
					system.debug((' bidContracted :: ' + bidContracted));
					Map<String, Task> contractTracesMap = new Map<String, Task>();
					for (Task trace : [
						SELECT Id, OwnerId, Subject, Status, ActivityDate, Priority, Order__c
						FROM Task
						WHERE WhatId = :bidContracted.Id AND Contract_Task__c = TRUE AND Subject != NULL
						ORDER BY Order__c ASC
					])
						contractTracesMap.put(trace.Subject, trace);
					system.debug('contactTracesMap after query :: ' + contractTracesMap);

					// uses the String identifier of the Button that came in combined with the service to execute actions based on button
					switch on relativeParentSObjectName {
						when 'Housing' {
							switch on documentUploadAction {
								when 'Contract' {
									Boolean firstContract = false;
									if (bidContracted.Contract_first_only__c == null && correlative < 1) {
										firstContract = true;
										update new Bid__c(Id = bidContracted.Id, Contract_first_only__c = true);
									}
                                    /**178134501
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Contract')) {
										if (firstContract)
											traceTasks.add(
												new Task(Id = contractTracesMap.get('Pending Contract').Id, Status = 'Completed', ActivityDate = null)
											);
										else if (contractTracesMap.containsKey('Pending Revised Contract'))
											traceTasks.add(
												new Task(Id = contractTracesMap.get('Pending Revised Contract').Id, Status = 'Completed', ActivityDate = null)
											);
									}**/
                                    if(!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Contract')) {
                                        traceTasks.add(new Task(Id = contractTracesMap.get('Pending Contract').Id, Status = 'Completed', ActivityDate = null));
                                    }
									if (contractTracesMap.containsKey('Needs Proofing')) {
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Needs Proofing').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 1)
											)
										);
										JournalCreation.insertJournal(
											new List<JournalCreation.JournalEntry>{
												new JournalCreation.JournalEntry(
													'bid',
													bidContracted.Id,
													bidJournalRT,
													'Needs Proofing: Due Date is change to ' +
													(Datetime.newInstance(BusinessDate.AddBusinessDays(Date.today(), 1), Time.newInstance(0, 0, 0, 0)))
														.format('dd-MMM-YYYY')
												)
											}
										);
									}
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Contract Received.')
										}
									);
								}
								when 'ContractToClient' {
                                    //178801592
									//update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'Pending Client Signature');
									//update new Housing__c(Id = bidParentId, Status_CC__c = 'Pending Client Signature');
									if (contractTracesMap.containsKey('Needs Proofing') && contractTracesMap.get('Needs Proofing').ActivityDate != null) {
										traceTasks.add(new Task(Id = contractTracesMap.get('Needs Proofing').Id, Status = 'Completed', ActivityDate = null));
										JournalCreation.insertJournal(
											new List<JournalCreation.JournalEntry>{
												new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Needs Proofing.')
											}
										);
									}
									if (
										contractTracesMap.containsKey('Pending Revised Contract') &&
										contractTracesMap.get('Pending Revised Contract').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Revised Contract').Id, Status = 'Completed', ActivityDate = null)
										);
									if (contractTracesMap.containsKey('Pending Contract') && contractTracesMap.get('Pending Contract').ActivityDate != null)
										traceTasks.add(new Task(Id = contractTracesMap.get('Pending Contract').Id, Status = 'Completed', ActivityDate = null));
									if (contractTracesMap.containsKey('Need To Send To Client')) {
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Need To Send To Client').Id, Status = 'Open', 
                                                     ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 1))
										);
										JournalCreation.insertJournal(
											new List<JournalCreation.JournalEntry>{
												new JournalCreation.JournalEntry(
													'bid',
													bidContracted.Id,
													bidJournalRT,
													'Need To Send To Client: Due Date is change to ' +
													(Datetime.newInstance(BusinessDate.AddBusinessDays(Date.today(), 1), Time.newInstance(0, 0, 0, 0)))
														.format('dd-MMM-YYYY')
												)
											}
										);
									}
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Contract To Client Received.')
										}
									);
								}
								when 'Final' {
									update new Bid__c(Id = bidContracted.Id, Final_is_uploaded__c = true, Final_Status__c = 'Contracted');
									update new Housing__c(Id = bidParentId, Status_CC__c = 'Contracted');
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Final Contract Received.')
										}
									);
									if (
										contractTracesMap.containsKey('Pending Client Signature') &&
										contractTracesMap.get('Pending Client Signature').ActivityDate != null
									) {
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Client Signature').Id, Status = 'Completed', ActivityDate = null)
										);
										JournalCreation.insertJournal(
											new List<JournalCreation.JournalEntry>{
												new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Received client signed contract.')
											}
										);
									}
									if (
										contractTracesMap.containsKey('Pending Hotel Counter') &&
										contractTracesMap.get('Pending Hotel Counter').ActivityDate != null
									) {
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Hotel Counter').Id, Status = 'Completed', ActivityDate = null)
										);
										JournalCreation.insertJournal(
											new List<JournalCreation.JournalEntry>{
												new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Received Counter signed contract')
											}
										);
									}
									if (contractTracesMap.containsKey('Need to Send to Client'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Need to Send to Client').Id, Status = 'Completed', ActivityDate = null)
										);
									if (contractTracesMap.containsKey('Contract Due Date'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Contract Due Date').Id, Status = 'Completed', ActivityDate = null));
									if (contractTracesMap.containsKey('Awaiting Pick-Up') && contractTracesMap.get('Awaiting Pick-Up').ActivityDate == null)
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Awaiting Pick-Up').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(bidContracted.Housing__r.Date_Out__c, 1)
											)
										);
									if (
										contractTracesMap.containsKey('Post Report to Client') &&
										contractTracesMap.get('Post Report to Client').ActivityDate == null
									)
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Post Report to Client').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(bidContracted.Housing__r.Date_Out__c, 1)
											)
										);
									// contract due date trace will be added here
									// contract coordinattor initiated
									if (bidContracted.isFromTournament__c) {
										if (
											contractTracesMap.containsKey('Post Report to Client') &&
											contractTracesMap.get('Post Report to Client').ActivityDate == null
										)
											traceTasks.add(
												new Task(
													Id = contractTracesMap.get('Post Report to Client').Id,
													Status = 'Open',
													ActivityDate = BusinessDate.AddBusinessDays(bidContracted.Housing__r.Date_Out__c, 1)
												)
											);
										if (contractTracesMap.containsKey('Pending Booking Link')) {
											system.debug('should be creating task');
											traceTasks.add(
												new Task(
													Id = contractTracesMap.get('Pending Booking Link').Id,
													ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 2)
												)
											);
										}
									}
								}
								when 'DateChange' {
									update new Bid__c(Id = bidContracted.Id, Date_Change_is_uploaded__c = true);
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Date Change Received.')
										}
									);
									if (
										contractTracesMap.containsKey('Pending Date Change') &&
										contractTracesMap.get('Pending Date Change').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Date Change').Id, Status = 'Completed', ActivityDate = null)
										);
									if (contractTracesMap.containsKey('Pending Update') && contractTracesMap.get('Pending Update').ActivityDate != null)
										traceTasks.add(new Task(Id = contractTracesMap.get('Pending Update').Id, Status = 'Completed', ActivityDate = null));
								}
								when 'NoRoomsPU' {
									update new Bid__c(Id = bidContracted.Id, No_Rooms_PU_is_uploaded__c = true, Final_Status__c = 'No Rooms Picked-Up');
									update new Housing__c(Id = bidParentId, Status_CC__c = 'No Rooms Picked-Up');
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'No Rooms PU Received.')
										}
									);
									if (
										contractTracesMap.containsKey('Pending No Rooms Picked Up') &&
										contractTracesMap.get('Pending No Rooms Picked Up').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending No Rooms Picked Up').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'Cancellation' {
									update new Bid__c(Id = bidContracted.Id, Cancellation_is_uploaded__c = true, Final_Status__c = 'Cancelled');
									update new Housing__c(Id = bidParentId, Status_CC__c = 'Cancelled');
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Cancellation Received.')
										}
									);
									if (contractTracesMap.containsKey('Pending Cancellation') && contractTracesMap.get('Pending Cancellation').ActivityDate != null)
										traceTasks.add(new Task(Id = contractTracesMap.get('Pending Cancellation').Id, Status = 'Completed', ActivityDate = null));
                                    if(contractTracesMap.containsKey('Check-in Call'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Check-in Call').Id, Status = 'Completed', ActivityDate = null));
                                    if(contractTracesMap.containsKey('Check-In Call'))
                                    	traceTasks.add(new Task(Id = contractTracesMap.get('Check-In Call').Id, Status = 'Completed', ActivityDate = null));
                                    if (contractTracesMap.containsKey('Awaiting Pick-Up'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Awaiting Pick-Up').Id, Status = 'Completed', ActivityDate = null));
								}
								when 'GCIP' {
									update new Bid__c(Id = bidContracted.Id, GCIP_is_uploaded__c = true);
									if (contractTracesMap.containsKey('Awaiting GCIP') && contractTracesMap.get('Awaiting GCIP').ActivityDate != null)
										traceTasks.add(new Task(Id = contractTracesMap.get('Awaiting GCIP').Id, Status = 'Completed', ActivityDate = null));
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'GCIP Received.')
										}
									);
								}
								when 'RoomingList' {
									update new Bid__c(Id = bidContracted.Id, Rooming_List_is_uploaded__c = true);
									if (
										contractTracesMap.containsKey('Rooming List Reminder') &&
										contractTracesMap.get('Rooming List Reminder').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Rooming List Reminder').Id, Status = 'Completed', ActivityDate = null)
										);
									if (
										contractTracesMap.containsKey('Rooming List Due Date') &&
										contractTracesMap.get('Rooming List Due Date').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Rooming List Due Date').Id, Status = 'Completed', ActivityDate = null)
										);
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Rooming List Received.')
										}
									);
								}
								when 'ContractClientSigned' {
                                    //178134641
									update new Bid__c(Id = bidContracted.Id, Contract_Client_Signed__c = true, Final_Status__c = (String.isNotBlank(bidContracted.Final_Status__c) && 
										bidContracted.Final_Status__c.equalsIgnoreCase('Pending Client Signature') ? 'Pending Hotel Counter' : bidContracted.Final_Status__c));
									//if(contractTracesMap.containsKey('Pending Client Signature') && contractTracesMap.get('Pending Client Signature').ActivityDate != null) traceTasks.add(new Task(Id = contractTracesMap.get('Pending Client Signature').Id, Status = 'Completed', ActivityDate = null));
									if (contractTracesMap.containsKey('Pending Client Signature'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Client Signature').Id, Status = 'Completed', ActivityDate = null)
										);
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Contract Client Signed Received.')
										}
									);
								}
								when 'PickUpReport' {
									update new Bid__c(Id = bidContracted.Id, Pick_Up_Report_is_uploaded__c = true);
									if (contractTracesMap.containsKey('Awaiting Pick-Up') && contractTracesMap.get('Awaiting Pick-Up').ActivityDate != null)
										traceTasks.add(new Task(Id = contractTracesMap.get('Awaiting Pick-Up').Id, Status = 'Completed', ActivityDate = null));
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Pick Up Report Received.')
										}
									);
									if (
										contractTracesMap.containsKey('Post Report to Client') &&
										contractTracesMap.get('Post Report to Client').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Post Report to Client').Id, Status = 'Completed', ActivityDate = null)
										);
									JournalCreation.insertJournal(
										new List<JournalCreation.JournalEntry>{
											new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, 'Post Report to Client.')
										}
									);
								}
								when 'RateAgreement' {
									if (
										contractTracesMap.containsKey('Pending Rate Agreement') &&
										contractTracesMap.get('Pending Rate Agreement').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Rate Agreement').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'SignedCCAuth' {
									if (contractTracesMap.containsKey('Awaiting Billing'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Awaiting Billing').Id, Status = 'Completed', ActivityDate = null));
								}
								when 'ConfirmationNumbers' {
									if (contractTracesMap.containsKey('Awaiting Confirmation Numbers'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Awaiting Confirmation Numbers').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'BookingLink' {
									if (contractTracesMap.containsKey('Proof Booking Link'))
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Proof Booking Link').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 1)
											)
										);
									if (contractTracesMap.containsKey('Pending Booking Link'))
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Pending Booking Link').Id,
												Status = 'Completed',
												ActivityDate = null
											)
										);
								}
								when 'HotelConfirmations' {
									if (contractTracesMap.containsKey('Awaiting Confirmation Numbers'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Awaiting Confirmation Numbers').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when else {
								}
							}
						}
						when 'Ground' {
							switch on documentUploadAction {
								when 'Contract' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'In Contracting');
									update new Ground__c(Id = bidParentId, Status_Ground__c = 'In Contracting');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Contract'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Pending Contract').Id, Status = 'Completed', ActivityDate = null));
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Needs Proofing'))
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Needs Proofing').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 1)
											)
										);
									if (
										!contractTracesMap.isEmpty() &&
										contractTracesMap.containsKey('Pending Revised Contract') &&
										contractTracesMap.get('Pending Revised Contract').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Revised Contract').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'ContractToClient' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'In Contracting');
									update new Ground__c(Id = bidParentId, Status_Ground__c = 'In Contracting');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Needs Proofing'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Needs Proofing').Id, Status = 'Completed', ActivityDate = null));
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Revised Contract'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Revised Contract').Id, Status = 'Completed', ActivityDate = null)
										);
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Need to Send to Client'))
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Need to Send to Client').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 1)
											)
										);
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Client Signature'))
										traceTasks.add(
											new Task(
												Id = contractTracesMap.get('Pending Client Signature').Id,
												Status = 'Open',
												ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 7)
											)
										);
								}
								when 'ContractClientSigned' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'Pending Client Signature');
									update new Ground__c(Id = bidParentId, Status_Ground__c = 'Pending Client Signature');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Client Signature'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Client Signature').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'Final' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'Contracted');
									update new Ground__c(Id = bidParentId, Status_Ground__c = 'Contracted');
									if (
										!contractTracesMap.isEmpty() &&
										contractTracesMap.containsKey('Pending Counter') &&
										contractTracesMap.get('Pending Counter').ActivityDate != null
									)
										traceTasks.add(new Task(Id = contractTracesMap.get('Pending Counter').Id, Status = 'Completed', ActivityDate = null));
									if (
										!contractTracesMap.isEmpty() &&
										contractTracesMap.containsKey('Pending Client Signature') &&
										contractTracesMap.get('Pending Client Signature').ActivityDate != null
									)
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Client Signature').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'TripUpdate' {
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Trip Update'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Trip Update').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'Cancellation' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'Cancelled');
									update new Ground__c(Id = bidParentId, Status_Ground__c = 'Cancelled');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Pending Cancellation'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Pending Cancellation').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when else {
								}
							}
						}
						when 'Air' {
							switch on documentUploadAction {
								when 'NameList' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'In Contracting');
									update new Air__c(Id = bidParentId, Status__c = 'In Contracting');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Names & Final Payment Due'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Names & Final Payment Due').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when 'Contract' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'In Contracting');
									update new Air__c(Id = bidParentId, Status__c = 'In Contracting');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Contract Due Date'))
										traceTasks.add(new Task(Id = contractTracesMap.get('Contract Due Date').Id, Status = 'Completed', ActivityDate = null));
								}
								when 'DepositLOCSignedContract' {
									update new Bid__c(Id = bidContracted.Id, Final_Status__c = 'Contracted');
									update new Air__c(Id = bidParentId, Status__c = 'Contracted');
									if (!contractTracesMap.isEmpty() && contractTracesMap.containsKey('Acknowledgement of Contract'))
										traceTasks.add(
											new Task(Id = contractTracesMap.get('Acknowledgement of Contract').Id, Status = 'Completed', ActivityDate = null)
										);
								}
								when else {
								}
							}
						}
					}
				}
				// clay adding map for dupe Id error on list update
				Map<Id, Task> traceMap = new Map<Id, Task>();
				if (!traceTasks.isEmpty()) {
					for (Task t : traceTasks) {
						system.debug('t :: ' + t);
						traceMap.put(t.Id, t);
					}
					update traceMap.values();
				}

				String action = 'A file';
				if (!documentUploadAction.equals('normal'))
					for (ButtonWrapper button : documentButtons)
						if (button.uploadAction.equals(documentUploadAction))
							action = button.label;
				if (!relativeParentSObjectName.equals('Housing'))
					JournalCreation.insertJournal(
						new List<JournalCreation.JournalEntry>{
							new JournalCreation.JournalEntry('bid', bidContracted.Id, bidJournalRT, action + ' was uploaded to documents.')
						}
					);
			} catch (Exception e) {
				system.debug(e.getMessage() + e.getStackTraceString());
			}
		}
		fileName = '';
		fileBody = '';
		documentUploadAction = '';
		getDocuments();
	}

	public void DeleteDocument() {
		if (String.isNotBlank(fileId)) {
			delete [SELECT Id FROM ContentDocument WHERE Id = :fileId];
			list<Share__c> shareConfiguration = [SELECT Id FROM Share__c WHERE WhatID__c = :fileId];
			if (!shareConfiguration.isEmpty())
				delete shareConfiguration;
			getDocuments();
		}
		fileId = '';
	}

	public void RenameDocument() {
		if (String.isNotBlank(fileId) && String.isNotBlank(fileName)) {
			update new ContentDocument(Id = fileId, Title = fileName);
			getDocuments();
		}
		fileId = '';
		fileName = '';
	}

	public void ShareWithCustomers() {
		if (String.isNotBlank(linkId)) {
			update new ContentDocumentLink(Id = linkId, Visibility = 'AllUsers');
			if (relativeParentSObjectName.equals('Air'))
				upsert new Share__c(
					Id = String.isNotBlank(shareId) ? shareId : null,
					WhatID__c = fileId,
					RelativeID__c = relativeParentId,
					isForCustomers__c = isShared
				);
			else
				upsert new Share__c(
					Id = String.isNotBlank(shareId) ? shareId : null,
					WhatID__c = fileId,
					RelativeID__c = relativeRecordId,
					isForCustomers__c = isShared
				);
			getDocuments();
		}
		linkId = '';
		fileId = '';
		shareId = '';
	}

	public void ShareWithVendors() {
		if (String.isNotBlank(linkId)) {
			update new ContentDocumentLink(Id = linkId, Visibility = 'AllUsers');
			if (relativeParentSObjectName.equals('Air'))
				upsert new Share__c(
					Id = String.isNotBlank(shareId) ? shareId : null,
					WhatID__c = fileId,
					RelativeID__c = relativeParentId,
					isForVendors__c = isShared
				);
			else
				upsert new Share__c(
					Id = String.isNotBlank(shareId) ? shareId : null,
					WhatID__c = fileId,
					RelativeID__c = relativeRecordId,
					isForVendors__c = isShared
				);
			getDocuments();
		}
		linkId = '';
		fileId = '';
		shareId = '';
	}

	public void SendEmail() {
		System.debug(emailJSON);
		Map<String, Object> root = (Map<String, Object>) JSON.deserializeUntyped(emailJSON);
		try {
			List<String> emailToList = new List<String>();
			if (root.containsKey('emailTo'))
				for (String email : ((String) root.get('emailTo')).split(','))
					if (String.isNotBlank(email))
						emailToList.add(email.trim());
			List<String> emailCCList = new List<String>();
			if (root.containsKey('emailCC'))
				for (String email : ((String) root.get('emailCC')).split(','))
					if (String.isNotBlank(email))
						emailCCList.add(email.trim());
			List<String> emailBCCList = new List<String>();
			if (root.containsKey('emailBCC'))
				for (String email : ((String) root.get('emailBCC')).split(','))
					if (String.isNotBlank(email))
						emailBCCList.add(email.trim());
			if (!emailToList.isEmpty()) {
				List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
				Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
				switch on relativeParentSObjectName {
					when 'Ground' {
						List<Production_Associations__c> prodAssocAux = [
							SELECT Id, User__r.Name, User__r.Email
							FROM Production_Associations__c
							WHERE Production_Opp__c = :opportunityId AND User__c != NULL AND Team_Roles__c INCLUDES ('Primary GT Coordinator')
						];
						if (!prodAssocAux.isEmpty())
							mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux.get(0).User__r.Email));
					}
					when 'Air' {
						List<Production_Associations__c> prodAssocAux = [
							SELECT Id, User__r.Name, User__r.Email
							FROM Production_Associations__c
							WHERE Production_Opp__c = :opportunityId AND User__c != NULL AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
						];
						if (!prodAssocAux.isEmpty())
							mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux.get(0).User__r.Email));
					}
				}
				mail.setToAddresses(emailToList);
				if (!emailCCList.isEmpty())
					mail.setCcAddresses(emailCCList);
				if (!emailBCCList.isEmpty())
					mail.setBccAddresses(emailBCCList);
				if (root.containsKey('emailSubject'))
					mail.setSubject((String) root.get('emailSubject'));
				if (root.containsKey('emailBody'))
					mail.setHtmlBody((String) root.get('emailBody'));
				if (root.containsKey('emailAttachment')) {
					List<Object> emailAttachmentIdsJSON = (List<Object>) root.get('emailAttachment');
					Set<String> emailAttachmentIds = new Set<String>();
					for (Object emailAttachmentIdJSON : emailAttachmentIdsJSON)
						emailAttachmentIds.add((String) emailAttachmentIdJSON);
					List<Messaging.Emailfileattachment> fileAttachments = new List<Messaging.Emailfileattachment>();
					List<ContentVersion> files = [
						SELECT Id, ContentDocumentId, Title, PathOnClient, VersionData
						FROM ContentVersion
						WHERE ContentDocumentId = :emailAttachmentIds
					];
					for (ContentVersion file : files) {
						Messaging.Emailfileattachment efa = new Messaging.Emailfileattachment();
						efa.setFileName(file.PathOnClient.subString(2, file.PathOnClient.length()));
						efa.setBody(file.VersionData);
						fileAttachments.add(efa);
					}
					mail.setFileAttachments(fileAttachments);
				}
				myEmails.add(mail);
				Messaging.sendEmail(myEmails);
				emailMessage = 'Email sent successfully!';
			}
		} catch (Exception e) {
			emailMessage = e.getMessage();
		}
	}
	/**
	 * verifyWideAddress description
	 * @param  email email description
	 * @return       return description
	 */
	public static String verifyWideAddress(String email) {
		String oweaId;
		List<OrgWideEmailAddress> oweaList;
		if (Test.isRunningTest())
			oweaList = [SELECT Id FROM OrgWideEmailAddress WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c];
		else
			oweaList = [SELECT Id FROM OrgWideEmailAddress WHERE Address = :email];
		if (oweaList.isEmpty())
			oweaList = [SELECT Id FROM OrgWideEmailAddress WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c]; //Email default
		oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
		return oweaId;
	}

	public class DocumentWrapper {
		public String linkId { get; set; }
		public String fileId { get; set; }
		public String versionId { get; set; }
		public String shareId { get; set; }
		public String title { get; set; }
		public String extension { get; set; }
		public DateTime createdDate { get; set; }
		public Integer contentSize { get; set; }
		public Boolean isFromCommunity { get; set; }
		public Boolean isForCustomers { get; set; }
		public Boolean isForVendors { get; set; }

		public DocumentWrapper(String linkId, String fileId) {
			this.linkId = linkId;
			this.fileId = fileId;
			this.versionId = '';
			this.shareId = '';
			this.title = '';
			this.extension = '';
			this.createdDate = null;
			this.contentSize = 0;
			this.isFromCommunity = false;
			this.isForCustomers = false;
			this.isForVendors = false;
		}
	}

	public class ButtonWrapper {
		public String label { get; set; }
		public String action { get; set; }
		public String uploadAction { get; set; }

		public ButtonWrapper(String label, String action, String uploadAction) {
			this.label = label;
			this.action = action;
			this.uploadAction = uploadAction;
		}
	}
}```
