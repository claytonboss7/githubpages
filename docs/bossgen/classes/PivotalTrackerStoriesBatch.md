---
layout: default
title: PivotalTrackerStoriesBatch
parent: classes
---
# Metadata Type
classes


# Filename 
PivotalTrackerStoriesBatch


# Raw XML
```
global class PivotalTrackerStoriesBatch implements Database.Batchable<PivotalTrackerService.PivotalTrackerStory>, Database.AllowsCallouts, Database.Stateful {
	public String theResponse;
	public String theProjectId;
	public String pivotalTrackerProjectId;

	public Integer numberFailures = 0;
	public Integer numberSuccess = 0;
	public Integer numberTotal = 0;

	public Map<String, String> theResultsMap = new Map<String, String>();

	global PivotalTrackerStoriesBatch(String theStoriesJSON, String pivotalTrackerProjectId) {
		this.theResponse = theStoriesJSON;
		//this.theProjectId = theSFProjectId;
		this.pivotalTrackerProjectId = pivotalTrackerProjectId;
	}

	global List<PivotalTrackerService.PivotalTrackerStory> start(Database.BatchableContext BC) {
		// collect the batches of records or objects to be passed to execute
		return (PivotalTrackerService.PivotalTrackerStory[]) JSON.deserialize(
			theResponse,
			PivotalTrackerService.PivotalTrackerStory[].class
		);
	}

	global void execute(
		Database.BatchableContext BC,
		List<PivotalTrackerService.PivotalTrackerStory> scope
	) {
		// process each batch of records

		Integer currentFailures = numberFailures;
		Integer currentSuccess = numberSuccess;
		Integer currentTotal = numberTotal;

		system.debug('numberFailures' + numberFailures);
		system.debug('numberSuccess' + numberSuccess);
		system.debug('numberTotal' + numberTotal);

		system.debug('currentFailures' + currentFailures);
		system.debug('currentSuccess' + currentSuccess);
		system.debug('currentTotal' + currentTotal);

		Map<String, String> theResults = theResultsMap.size() > 0
			? theResultsMap
			: new Map<String, String>();

		system.debug('theResults' + theResults);

		try {
			PivotalTrackerService.PivotalTrackerStory story = scope[0];
			story.labels = null;
			story.owned_by_id = null;
			story.project_id = Integer.valueOf(pivotalTrackerProjectId);
			story.id = null;
			story.url = null;
			story.requested_by_id = null;
			story.accepted_at = null;
			String theJSON = JSON.serialize(story, true);
			PivotalTrackerService.PivotalTrackerStory storyFinal = story;
			PivotalTrackerService.PivotalTrackerStory[] stories = PivotalTrackerService.PT_EndPoint_Stories(
				'POST',
				pivotalTrackerProjectId,
				null,
				new List<PivotalTrackerService.PivotalTrackerStory>{ storyFinal }
			);
			system.debug(stories);
			for (PivotalTrackerService.PivotalTrackerStory stry : stories) {
				system.debug(stry);
				Map<String, Object> theMap = (Map<String, Object>) JSON.deserialize(
					JSON.serialize(stry),
					Map<String, Object>.class
				);
				system.debug(theMap);
				if (theMap.containsKey('error')) {
					currentFailures = currentFailures + 1;
					theResults.put('error', String.valueOf(theMap.get('error')));
				} else {
					currentSuccess = currentSuccess + 1;
					theResults.put('success', String.valueOf(stry));
				}
				currentTotal = currentTotal + 1;
			}
		} catch (Exception e) {
			currentFailures = currentFailures + 1;
			System.debug('Error-' + e.getMessage());
		}

		theResultsMap = theResults;

		numberFailures = currentFailures;
		numberSuccess = currentSuccess;
		numberTotal = currentTotal;

		system.debug('theResultsMap' + theResultsMap);
		system.debug('numberFailures' + numberFailures);
		system.debug('numberSuccess' + numberSuccess);
		system.debug('numberTotal' + numberTotal);
	}
	global void finish(Database.BatchableContext BC) {
		// execute any post-processing operations
		Map<String, String> theResultsFinish = new Map<String, String>();
		theResultsFinish = theResultsMap;

		Messaging.SingleEmailMessage message = new Messaging.SingleEmailMessage();
		message.toAddresses = new List<String>{ 'claytonboss@gmail.com' };
		message.subject = 'Results of Pivotal Tracker Sync';
		message.plainTextBody = 'subject';
		message.htmlbody =
			theResultsFinish.toString() +
			'

Failures: ' +
			numberFailures +
			'

Success: ' +
			numberSuccess +
			'

Total: ' +
			numberTotal;
		Messaging.SingleEmailMessage[] messages = new List<Messaging.SingleEmailMessage>{ message };
		Messaging.SendEmailResult[] results = Messaging.sendEmail(messages);
		if (results[0].success) {
			System.debug('The email was sent successfully.');
		} else {
			System.debug('The email failed to send: ' + results[0].errors[0].message);
		}
	}
}
```


# Last Modified


# Usage
