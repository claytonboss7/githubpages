---
layout: default
title: PivotalTrackerService
parent: classes
---
# Metadata Type
classes


# Filename 
PivotalTrackerService


# Raw XML
```
/**
 * @description       : 
 * @author            : sfdc cb
 * @group             : 
 * @last modified on  : 10-06-2021
 * @last modified by  : sfdc cb
**/
global class PivotalTrackerService {
	public PivotalTrackerService() {
	}

	public static final String theNamedCredential = 'Pivotal_Tracker';
	public static final integer STORY_LIMIT = 1000;
	public static String thePivotalProjectId = '';
	public static String theSFProject = '';

	/** the HTTP callout to Pivotal Tracker that happens during various sync activities
	 * @param  thePath the base url for the API is stored in the Named Credential and the path is the specific endpoint we are calling
	 * @param  theBody string body for POST requests
	 * @param  method  GET / POST / PUT / DELETE / PATCH
	 * @param  headers some endpoints require specific headers so we feed them in in their respective createXXXXX method
	 *                                                                                                                               */
	public static String PT_Service_Callout(
		String theMethodName,
		String thePath,
		String theBody,
		String method,
		Map<String, String> headers
	) {
		return doHTTP(theMethodName, thePath, theBody, method, headers);
	}

	/* parse methods - these allow deserialization by type with a naming convention */
	public static PivotalTrackerStory[] PT_Utils_Parse_Stories(
		String pivotalTrackerProjectId,
		String method,
		List<String> params,
		PivotalTrackerService.PivotalTrackerStory[] stories
	) {
		system.debug('stories :: ' + stories);

		PivotalTrackerStory[] theStories = new List<PivotalTrackerStory>(
			(PivotalTrackerStory[]) JSON.deserialize(
				PT_Service_Callout(
					'PT_EndPoint_Stories',
					method == 'GET'
						? String.format(
								ptEndPointReferenceMap.get('PT_EndPoint_Stories'),
								new List<String>{ pivotalTrackerProjectId, '?limit=1000&after_story_id=500' }
						  )
						: method == 'PUT' ? String.format(
								ptEndPointReferenceMap.get('PT_EndPoint_Stories'),
								new List<String>{ pivotalTrackerProjectId, String.valueOf('/'+stories[0].id) }
						  ) : String.format(
									ptEndPointReferenceMap.get('PT_EndPoint_Stories'),
									new List<String>{ pivotalTrackerProjectId, '?limit=1000&after_story_id=500' }
								),
					method == 'POST' || method == 'PUT' && stories.size() > 0 ? System.JSON.serialize(stories[0], true) : null,
					method,
					getHeaders()
				),
				PivotalTrackerStory[].class
			)
		);
		return theStories;
	}
	
	public static PivotalTrackerStory PT_Utils_Parse_Story(
		String pivotalTrackerProjectId,
		String pivotalTrackerStoryId,
		String method,
		List<String> params
	) {
		return (PivotalTrackerStory) JSON.deserialize(
			PT_Service_Callout(
				'PT_EndPoint_Story',
				String.format(ptEndPointReferenceMap.get('PT_EndPoint_Story'), params),
				null,
				method,
				getHeaders()
			),
			PivotalTrackerStory.class
		);
	}
	public static PivotalTrackerProject PT_Utils_Parse_Projects(
		PivotalTrackerProject thePivotalProject,
		String method
	) {
		system.debug('thePivotalProject :: ' + thePivotalProject);
		return (PivotalTrackerProject) JSON.deserialize(
			PT_Service_Callout(
				'PT_EndPoint_Projects',
				ptEndPointReferenceMap.get('PT_EndPoint_Projects'),
				method == 'POST' ? JSON.serialize(thePivotalProject, true) : null,
				method,
				getHeaders()
			),
			PivotalTrackerProject.class
		);
	}
	public static PivotalTrackerProject[] PT_Utils_Parse_Projects(
		PivotalTrackerProject thePivotalProject,
		PivotalTrackerService.PivotalTrackerAccount[] accountIds,
		String method
	) {
		system.debug('thePivotalProject :: ' + thePivotalProject);
		return (PivotalTrackerProject[]) JSON.deserialize(
			PT_Service_Callout(
				'PT_EndPoint_Projects',
				ptEndPointReferenceMap.get('PT_EndPoint_Projects'),
				method == 'POST' ? JSON.serialize(thePivotalProject, true) : null,
				method,
				getHeaders()
			),
			PivotalTrackerProject[].class
		);
	}
	public static PivotalTrackerProject PT_Utils_Parse_Project(
		PivotalTrackerService.PivotalTrackerProject project_id,
		String method
	) {
		String thePivotalProjectId = String.valueOf(project_id.id);
		return (PivotalTrackerProject) JSON.deserialize(
			PT_Service_Callout(
				'PT_EndPoint_Project',
				String.format(
					ptEndPointReferenceMap.get('PT_EndPoint_Project'),
					new List<String>{ thePivotalProjectId }
				),
				null,
				method,
				getHeaders()
			),
			PivotalTrackerProject.class
		);
	}
	public static PivotalTrackerIteration[] PT_Utils_Parse_Iterations(Integer thePivotalProjectId) {
		PivotalTrackerIteration[] theIterations;
		String endpointString = String.format(
			ptEndPointReferenceMap.get('PT_EndPoint_Iterations'),
			new List<String>{ String.valueOf(thePivotalProjectId), '?limit=1000' }
		);
		String theResponse = PT_Service_Callout(
			'PT_EndPoint_Iterations',
			endpointString,
			null,
			'GET',
			getHeaders()
		);
		theIterations = PivotalTrackerIteration.parse(theResponse);
		for (PivotalTrackerIteration ptii : theIterations) {
		}
		return theIterations;
	}
	public static PivotalTrackerIteration[] PT_Utils_Parse_Iterations(
		Integer thePivotalProjectId,
		String theScope
	) {
		PivotalTrackerIteration[] theIterations;
		String endpointString = String.format(
			ptEndPointReferenceMap.get('PT_EndPoint_Iterations'),
			new List<String>{ String.valueOf(thePivotalProjectId), '?limit=1000&scope=' + theScope }
		);
		String theResponse = PT_Service_Callout(
			'PT_EndPoint_Iterations',
			endpointString,
			null,
			'GET',
			getHeaders()
		);
		theIterations = PivotalTrackerIteration.parse(theResponse);
		for (PivotalTrackerIteration ptii : theIterations) {
		}
		return theIterations;
	}
	/* endpoints - https://www.pivotaltracker.com/help/api/rest/v5#Endpoints */
	/**
	 * PT_EndPoint_Stories description
	 * @param  method    GET, POST
	 * @param  pivotalTrackerProjectId pivotalTrackerProjectId
	 * @param  stories   stories description
	 * @return           return description
	 */
	public static PivotalTrackerStory[] PT_EndPoint_Stories(
		String method,
		String pivotalTrackerProjectId,
		String pivotalTrackerStoryId,
		PivotalTrackerStory[] stories
	) {
		return PT_Utils_Parse_Stories(
			pivotalTrackerProjectId,
			method,
			new List<String>(),
			method == 'POST' || method == 'PUT' ? stories : new List<PivotalTrackerService.PivotalTrackerStory>()
		);
	}
	public static PivotalTrackerIteration[] PT_EndPoint_Iterations(
		String method,
		String pivotalTrackerProjectId
	) {
		PivotalTrackerProject ptProject = new PivotalTrackerProject();
		ptProject.id = Integer.valueOf(pivotalTrackerProjectId);
		return PT_Utils_Parse_Iterations(ptProject.id);
	}
	public static PivotalTrackerIteration[] PT_EndPoint_Iterations(
		String method,
		String pivotalTrackerProjectId,
		String scope
	) {
		PivotalTrackerProject ptProject = new PivotalTrackerProject();
		ptProject.id = Integer.valueOf(pivotalTrackerProjectId);
		return PT_Utils_Parse_Iterations(ptProject.id,scope);
	}
	/**
	 * PT_EndPoint_Story endpoint to update, view, delete a story
	 * @param  method    update, view, DELETE
	 * @param  thePivotalProjectId the externalId for PT
	 * @param  stories   the payLoad
	 * @return           returns resource PivotalTrackerStory[]
	 */
	public static PivotalTrackerStory PT_EndPoint_Story(
		String method,
		String pivotalTrackerProjectId,
		String pivotalTrackerStoryId,
		String[] details
	) {
		return PT_Utils_Parse_Story(
			pivotalTrackerProjectId,
			PivotalTrackerStoryId,
			method,
			new List<String>{ pivotalTrackerProjectId, pivotalTrackerStoryId }
		);
	}
	/**
	 * Fetch and Create Projects
	 * @param  pivotalTrackerAccountIds API requires a set of IDs to fetch projects for
	 * @param  method                   GET , PUT
	 * @return                          list of Projects from PivotalTracker
	 */
	public static PivotalTrackerProject[] PT_Endpoint_Projects(
		PivotalTrackerProject thePivotalProject,
		PivotalTrackerService.PivotalTrackerAccount[] pivotalTrackerAccountIds,
		String method
	) {
		return PT_Utils_Parse_Projects(thePivotalProject, pivotalTrackerAccountIds, method);
	}
	public static PivotalTrackerProject PT_Endpoint_Projects(
		PivotalTrackerProject thePivotalProject,
		String method
	) {
		return PT_Utils_Parse_Projects(thePivotalProject, method);
	}
	/**
	 * Fetch and Update and Delete Projects
	 * @param  pivotalTrackerAccountIds API requires a set of IDs to fetch projects for
	 * @param  method                   GET , PUT, DELETE
	 * @return                          list of Projects from PivotalTracker
	 */
	public static PivotalTrackerProject PT_Endpoint_Project(
		PivotalTrackerService.PivotalTrackerProject project_id,
		String method
	) {
		return PT_Utils_Parse_Project(project_id, method);
	}

	public static Map<String, String> ptEndPointReferenceMap = new Map<String, String>{
		'PT_EndPoint_Stories' => '/projects/{0}/stories{1}',
		'PT_EndPoint_Iterations' => '/projects/{0}/iterations{1}',
		'PT_EndPoint_Story' => '/projects/{0}/stories/{1}',
		'PT_EndPoint_Projects' => '/projects',
		'PT_EndPoint_Project' => '/projects/{0}'
	};

	public static String doHTTP(
		String theMethodName,
		String thePath,
		String theBody,
		String method,
		Map<String, String> headers
	) {
		system.debug('called by :: ' + theMethodName);
		system.debug('the body :: ' + theBody);
		HttpRequest req = new HttpRequest();
		req.setEndpoint('callout:' + theNamedCredential + thePath);
		req.setHeader('X-TrackerToken', '{!$Credential.Password}');
		req.setMethod(method);
		req.setHeader('Connection', 'keep-alive');
		req.setHeader('Content-Type', 'application/json');
		req.setTimeout(120000);
		if (method != null && method != '' && method == 'POST' || method == 'PUT')
			req.setHeader('Content-Length', String.valueOf(theBody.length()));
		if (headers.size() > 0) {
			for (String header : headers.keySet()) {
				req.setHeader(header, headers.get(header));
			}
		}
		if (theBody != null) {
			req.setBody(theBody);
		}

		if (theBody != null) {
			system.debug('bod not null - ' + theBody);
		}
		system.debug(req);
		Http http = new Http();
		HTTPResponse res = http.send(req);
		System.debug(res.getBody());
		System.debug(res.getBody());

		String theResponse = res.getBody();
		return theResponse;
	}

	/* CRUD muffins */
	public static PivotalTrackerService.PivotalTrackerProject PT_CRUD_createProject(
		String theProjectSFId,
		PivotalTrackerProject theProjectToCreate
	) {
		Project__c existingProject = [
			SELECT Account__r.Name, Name, Id, Project_Id__c
			FROM Project__c
			WHERE Id = :theProjectSFId
		];
		String pivotalTrackerId = existingProject != null
			? existingProject.Project_Id__c
			: existingProject.Project_Id__c;
		PivotalTrackerService.PivotalTrackerProject theProject;
		theProjectToCreate.name = existingProject.Name + ' - Salesforce';
		String theResult = '';
		if (existingProject != null && existingProject.Project_Id__c != null) {
			theResult =
				'A Project with Id ' +
				pivotalTrackerId +
				' is already associated to this SF Project - existingProject.Name - can not continue';
		} else if (existingProject != null && existingProject.Project_Id__c == null) {
			theProject = PT_Endpoint_Projects(theProjectToCreate, 'POST');
		}
		return theProject;
	}

	public static PivotalTrackerProject[] PT_Utils_JSON_to_PivotalTrackerProjectObject(
		String theProjectJSON
	) {
		return ((PivotalTrackerService.PivotalTrackerProject[]) JSON.deserialize(
			theProjectJSON,
			PivotalTrackerService.PivotalTrackerProject[].class
		));
	}

	public static PivotalTrackerAccount[] PT_Utils_JSON_to_PivotalTrackerAccountObject(
		String theAccountJSON
	) {
		return ((PivotalTrackerService.PivotalTrackerAccount[]) JSON.deserialize(
			theAccountJSON,
			PivotalTrackerService.PivotalTrackerAccount[].class
		));
	}

	public static Project_Item__c[] PT_Utils_JSON_to_ProjectItemsSObjectList(String theStoriesJSON) {
		//Map<String, Object> data = (Map<String, Object>)JSON.deserializeUntyped(theStoriesJSON);
		//Object theJSON = data.get('stories');

		PivotalTrackerService.PivotalTrackerStory[] stories = (PivotalTrackerService.PivotalTrackerStory[]) System.JSON.deserialize(
			theStoriesJSON,
			PivotalTrackerService.PivotalTrackerStory[].class
		);
		List<Project_Item__c> projectItemsToUpsert = new List<Project_Item__c>();
		system.debug(stories.size());
		for (PivotalTrackerService.PivotalTrackerStory story : stories) {
			Project_Item__c pItem = new Project_Item__c(
				pt_id__c = story.id,
				pt_name__c = story.name.left(255),
				pt_updated_at__c = story.updated_at,
				pt_estimate__c = story.estimate,
				pt_created_at__c = story.created_at,
				pt_kind__c = story.kind,
				pt_current_state__c = story.current_state,
				pt_url__c = story.url,
				Story_Id__c = String.valueOf(story.id),
				Data__c = story.toString(),
				URL__c = story.url,
				Kind__c = story.kind,
				Story_Name__c = story.name.left(255),
				Story_Status__c = story.current_state,
				Project__c = [SELECT Id FROM Project__c WHERE Name = 'Road Rebel'].Id
			);
			projectItemsToUpsert.add(pItem);
		}
		upsert projectItemsToUpsert pt_id__c;
		return projectItemsToUpsert;
	}
	/*

    static PivotalTrackerProject[] PT_Endpoint_Account(String projectId, String theBody, PivotalTrackerProject[] stories){
    }

    static PivotalTrackerProject[] PT_Endpoint_Accounts(String projectId, String theBody, PivotalTrackerProject[] stories){
    }

    static PivotalTrackerProject[] PT_Endpoint_Account_Memberships(String projectId, String theBody, PivotalTrackerProject[] stories){
    }
*/
	public static PivotalTrackerService.PivotalTrackerStory[] PT_Utils_Copy_PTProject_To_SFProject(
		String pivotalTrackerProjectId
	) {
		PivotalTrackerService.PivotalTrackerStory[] theStories = PT_EndPoint_Stories(
			'GET',
			pivotalTrackerProjectId,
			null,
			new List<PivotalTrackerService.PivotalTrackerStory>()
		);
		system.debug('theStories :: ' + theStories.size());
		return theStories;
	}

	public static String PT_Utils_Copy_Stories_PTProject_To_PTProject(
		String pivotalTrackerSourceProjectId,
		String pivotalTrackerTargetProjectId
	) {
		PivotalTrackerService.PivotalTrackerStory[] theStories = PT_EndPoint_Stories(
			'GET',
			pivotalTrackerSourceProjectId,
			null,
			new List<PivotalTrackerService.PivotalTrackerStory>()
		);
		system.debug('theStories :: ' + theStories.size());
		PivotalTrackerStoriesBatch ptsb = new PivotalTrackerStoriesBatch(
			JSON.serialize(theStories),
			pivotalTrackerTargetProjectId
		);
		return Database.executeBatch(ptsb, 1);
	}

	public static PivotalTrackerStoryResult getStories(Integer projectId) {
		PivotalTrackerStoryResult res = new PivotalTrackerStoryResult();
		res.projectId = projectId;
		res.tracker = new PivotalTrackerService();
		return res.next();
	}

	public static Map<String, String> getHeaders() {
		return new Map<String, String>{
			'Connection' => 'keep-alive',
			'Content-Type' => 'application/json'
		};
	}

	public static String getStoriesByProject(String projectId) {
		String theJSONData = PT_Service_Callout(
			'getStoriesByProject',
			'/projects/' +
			projectId +
			'/stories?limit=1000',
			null,
			'GET',
			new Map<String, String>()
		);
		system.debug(theJSONData);
		return theJSONData;
	}

	public static void getProjectById(String theProjectId) {
	}

	public static void createStories(String theResponse, String projectId) {
		//system.debug(theResponse);

		List<PivotalTrackerStory> stories = (List<PivotalTrackerStory>) JSON.deserialize(
			theResponse,
			List<PivotalTrackerStory>.class
		);
		List<PivotalTrackerStory> finalStories = new List<PivotalTrackerStory>();
		for (PivotalTrackerStory story : stories) {
			story.id = null;
			story.owner_ids = null;
			//story.description = null;
			story.accepted_at = null;
			story.updated_at = null;
			story.owned_by_id = null;
			String storyString = JSON.serialize(story, true);
			PivotalTrackerStory theStory = (PivotalTrackerStory) JSON.deserialize(
				storyString,
				PivotalTrackerStory.class
			);
			if (theStory.name != null && theStory.name != '') {
				finalStories.add(theStory);
				PT_Service_Callout(
					'createStories',
					'/projects/' +
					projectId +
					'/stories',
					storyString,
					'POST',
					new Map<String, String>{ 'X-Tracker-Project-Version' => '1' }
				);
			}
		}
	}
	/**
	 * used to create a project via the Pivotal Tracker API, called by Copy and Seed mechanisms
	 */
	public static void createProject(
		String projectSFId,
		Integer id,
		String kind,
		String name,
		String description,
		String profile_content,
		Integer version,
		Integer iteration_length,
		String week_start_day,
		String point_scale,
		Boolean point_scale_is_custom,
		Boolean bugs_and_chores_are_estimatable,
		Boolean automatic_planning,
		Boolean enable_tasks,
		Integer velocity_averaged_over,
		Integer number_of_done_iterations_to_show,
		Boolean has_google_domain,
		Boolean enable_incoming_emails,
		Integer initial_velocity,
		Boolean public_Z,
		Boolean atom_enabled,
		String project_type,
		String start_time,
		String created_at,
		String updated_at,
		Integer account_id,
		Integer current_iteration_number,
		Boolean enable_following,
		String status,
		Date start_date,
		String join_as
	) {
		PivotalTrackerProject theNewProject = new PivotalTrackerProject();

		theNewProject.account_id = account_id;
		theNewProject.atom_enabled = atom_enabled;
		theNewProject.automatic_planning = automatic_planning;
		theNewProject.bugs_and_chores_are_estimatable = bugs_and_chores_are_estimatable;
		theNewProject.created_at = created_at;
		theNewProject.current_iteration_number = current_iteration_number;
		theNewProject.description = description;
		theNewProject.enable_following = enable_following;
		theNewProject.enable_incoming_emails = enable_incoming_emails;
		theNewProject.enable_tasks = enable_tasks;
		//theNewProject.epic_ids = epic_ids;
		theNewProject.has_google_domain = has_google_domain;
		theNewProject.id = id;
		theNewProject.initial_velocity = initial_velocity;
		//theNewProject.integration_ids = integration_ids;
		theNewProject.iteration_length = iteration_length;
		//theNewProject.iteration_override_numbers = iteration_override_numbers;
		theNewProject.join_as = join_as;
		theNewProject.kind = kind;
		//theNewProject.label_ids = label_ids;
		//theNewProject.membership_ids = membership_ids;
		theNewProject.name = name;
		theNewProject.number_of_done_iterations_to_show = number_of_done_iterations_to_show;
		theNewProject.point_scale = point_scale;
		theNewProject.point_scale_is_custom = point_scale_is_custom;
		theNewProject.profile_content = profile_content;
		theNewProject.project_type = project_type;
		theNewProject.public_Z = public_Z;
		//theNewProject.review_type_ids = review_type_ids;
		theNewProject.start_date = start_date;
		theNewProject.start_time = start_time;
		theNewProject.status = status;
		//theNewProject.story_ids = story_ids;
		// theNewProject.story_template_ids = story_template_ids;
		theNewProject.updated_at = updated_at;
		theNewProject.velocity_averaged_over = velocity_averaged_over;
		theNewProject.version = version;
		theNewProject.week_start_day = week_start_day;

		String theBody = theNewProject.toString().replaceAll('_Z', '');
		theBody = JSON.serialize(theNewProject, true);
		theBody = theBody.trim();
		system.debug(theBody);
		String theJSONResponse = PT_Service_Callout(
			'createProject',
			'/projects',
			theBody,
			'POST',
			new Map<String, String>{ 'X-Tracker-Project-Version' => '1' }
		);
		/*PivotalTrackerService.PivotalTrackerProject project = (PivotalTrackerService.PivotalTrackerProject) JSON.deserialize(theJSONResponse, PivotalTrackerService.PivotalTrackerProject.class);
        system.debug (project);
        Project__c updateProject = new Project__c(
            Id = projectSFId,
            Project_Id__c = String.valueOf(project.id)
        );
        update updateProject;*/
	}
	/**
	 * getHTTPRequestPivotalTracker description
	 * @param  thePath thePath description
	 * @param  theBody theBody description
	 * @param  method  method description
	 * @param  headers headers description
	 * @return         return description
	 */
	public HttpRequest getHTTPRequestPivotalTracker(
		String thePath,
		String theBody,
		String method,
		Map<String, String> headers
	) {
		return null;
	}

	/**
	 * sendHTTPResponsePivotalTracker description
	 * @param  req req description
	 * @return     return description
	 */
	public HTTPResponse sendHTTPResponsePivotalTracker(HttpRequest req) {
		Http http = new Http();
		HTTPResponse res = http.send(req);
		System.debug(res.getBody());
		return res;
	}

	/* Pivotal Tracker Objects Below */

	global class PivotalTrackerProject {
		public Integer id { get; set; }
		public String kind { get; set; }
		public String name { get; set; }
		public String description { get; set; }
		public String profile_content { get; set; }
		public Integer version { get; set; }
		public Integer iteration_length { get; set; }
		public String week_start_day { get; set; }
		public String point_scale { get; set; }
		public Boolean point_scale_is_custom { get; set; }
		public Boolean bugs_and_chores_are_estimatable { get; set; }
		public Boolean automatic_planning { get; set; }
		public Boolean enable_tasks { get; set; }
		//public Time_zone time_zone {get;set;}
		public Integer velocity_averaged_over { get; set; }
		public Integer number_of_done_iterations_to_show { get; set; }
		public Boolean has_google_domain { get; set; }
		public Boolean enable_incoming_emails { get; set; }
		public Integer initial_velocity { get; set; }
		public Boolean public_Z { get; set; } // in json: public
		public Boolean atom_enabled { get; set; }
		public String project_type { get; set; }
		public String start_time { get; set; }
		public String created_at { get; set; }
		public String updated_at { get; set; }
		public Integer account_id { get; set; }
		public Integer current_iteration_number { get; set; }
		public Boolean enable_following { get; set; }
		public String status { get; set; }
		public Date start_date { get; set; }
		public String join_as { get; set; }
		public List<Integer> story_ids { get; set; }
		public List<Integer> epic_ids { get; set; }
		public List<Integer> membership_ids { get; set; }
		public List<Integer> label_ids { get; set; }
		public List<Integer> integration_ids { get; set; }
		public List<Integer> review_type_ids { get; set; }
		public List<Integer> story_template_ids { get; set; }
		public List<Integer> iteration_override_numbers { get; set; }

		public PivotalTrackerProject() {
		}
	}

	global class PivotalTrackerStory {
		public String kind;
		public Integer id;
		public String created_at;
		public String updated_at;
		public String accepted_at;
		public Integer estimate;
		public String story_type;
		public String name;
		public String current_state;
		public Integer requested_by_id;
		public String url;
		public Integer project_id;
		public List<Integer> owner_ids;
		public List<PivotalTrackerLabel> labels;
		public Integer owned_by_id;
		public String description;
	}

	global class PivotalTrackerLabel {
		public Integer id;
		public Integer project_id;
		public String kind;
		public String name;
		public String created_at;
		public String updated_at;
	}
	public class PivotalTrackerStoryResult {
		public List<PivotalTrackerStory> stories;
		public Integer offset = 0;
		public PivotalTrackerService tracker;
		public Integer projectId;
		public PivotalTrackerStoryResult next() {
			String url = '/projects/' + projectId + '/stories?limit=' + STORY_LIMIT + '&offset=' + offset;
			system.debug('url :: ' + url);
			String theStories = PT_Service_Callout('next', url, null, 'GET', new Map<String, String>());
			system.debug(theStories);
			stories = (List<PivotalTrackerStory>) System.JSON.deserialize(
				theStories,
				List<PivotalTrackerStory>.class
			);
			system.debug('theStories :: ' + theStories);
			offset = offset + STORY_LIMIT;
			return this;
		}
	}
	global class PivotalTrackerAccount {
		Integer id { get; set; }
		String name { get; set; }
		String plan { get; set; }
		String status { get; set; }
		Integer days_left { get; set; }
		Boolean over_the_limit { get; set; }
		Datetime created_at { get; set; }
		Datetime updated_at { get; set; }
		Integer[] project_ids { get; set; }
		String kind { get; set; }
	}
	global class PivotalTrackerAccount_Membership {
		Integer id { get; set; }
		String name { get; set; }
		String plan { get; set; }
		String status { get; set; }
		Integer days_left { get; set; }
		Boolean over_the_limit { get; set; }
		Datetime created_at { get; set; }
		Datetime updated_at { get; set; }
		Integer[] project_ids { get; set; }
		String kind { get; set; }
	}
	public class Stories_Z {
		public Stories_Z(JSONParser parser) {
			while (parser.nextToken() != System.JSONToken.END_OBJECT) {
				if (parser.getCurrentToken() == System.JSONToken.FIELD_NAME) {
					String text = parser.getText();
					if (parser.nextToken() != System.JSONToken.VALUE_NULL) {
						{
							System.debug(LoggingLevel.WARN, 'Stories_Z consuming unrecognized property: ' + text);
							consumeObject(parser);
						}
					}
				}
			}
		}
	}
	public class Labels {
		public Integer id { get; set; }
		public Integer project_id { get; set; }
		public String kind { get; set; }
		public String name { get; set; }
		public String created_at { get; set; }
		public String updated_at { get; set; }

		public Labels(JSONParser parser) {
			while (parser.nextToken() != System.JSONToken.END_OBJECT) {
				if (parser.getCurrentToken() == System.JSONToken.FIELD_NAME) {
					String text = parser.getText();
					if (parser.nextToken() != System.JSONToken.VALUE_NULL) {
						if (text == 'id') {
							id = parser.getIntegerValue();
						} else if (text == 'project_id') {
							project_id = parser.getIntegerValue();
						} else if (text == 'kind') {
							kind = parser.getText();
						} else if (text == 'name') {
							name = parser.getText();
						} else if (text == 'created_at') {
							created_at = parser.getText();
						} else if (text == 'updated_at') {
							updated_at = parser.getText();
						} else {
							System.debug(LoggingLevel.WARN, 'Labels consuming unrecognized property: ' + text);
							consumeObject(parser);
						}
					}
				}
			}
		}
	}
	public class Stories {
		public String kind { get; set; }
		public Integer id { get; set; }
		public String created_at { get; set; }
		public String updated_at { get; set; }
		public String accepted_at { get; set; }
		public Integer estimate { get; set; }
		public String story_type { get; set; }
		public String name { get; set; }
		public String description { get; set; }
		public String current_state { get; set; }
		public Integer requested_by_id { get; set; }
		public String external_id { get; set; }
		public Integer integration_id { get; set; }
		public String url { get; set; }
		public Integer project_id { get; set; }
		public List<Integer> owner_ids { get; set; }
		public List<Labels> labels { get; set; }
		public Integer owned_by_id { get; set; }

		public Stories(JSONParser parser) {
			while (parser.nextToken() != System.JSONToken.END_OBJECT) {
				if (parser.getCurrentToken() == System.JSONToken.FIELD_NAME) {
					String text = parser.getText();
					if (parser.nextToken() != System.JSONToken.VALUE_NULL) {
						if (text == 'kind') {
							kind = parser.getText();
						} else if (text == 'id') {
							id = parser.getIntegerValue();
						} else if (text == 'created_at') {
							created_at = parser.getText();
						} else if (text == 'updated_at') {
							updated_at = parser.getText();
						} else if (text == 'accepted_at') {
							accepted_at = parser.getText();
						} else if (text == 'estimate') {
							estimate = parser.getIntegerValue();
						} else if (text == 'story_type') {
							story_type = parser.getText();
						} else if (text == 'name') {
							name = parser.getText();
						} else if (text == 'description') {
							description = parser.getText();
						} else if (text == 'current_state') {
							current_state = parser.getText();
						} else if (text == 'requested_by_id') {
							requested_by_id = parser.getIntegerValue();
						} else if (text == 'external_id') {
							external_id = parser.getText();
						} else if (text == 'integration_id') {
							integration_id = parser.getIntegerValue();
						} else if (text == 'url') {
							url = parser.getText();
						} else if (text == 'project_id') {
							project_id = parser.getIntegerValue();
						} else if (text == 'owner_ids') {
							owner_ids = arrayOfInteger(parser);
						} else if (text == 'labels') {
							labels = arrayOfLabels(parser);
						} else if (text == 'owned_by_id') {
							owned_by_id = parser.getIntegerValue();
						} else {
							System.debug(LoggingLevel.WARN, 'Stories consuming unrecognized property: ' + text);
							consumeObject(parser);
						}
					}
				}
			}
		}
	}
	public static List<PivotalTrackerIteration> parse(String json) {
		System.JSONParser parser = System.JSON.createParser(json);
		return arrayOfPivotalTrackerIterations(parser);
	}
	public static void consumeObject(System.JSONParser parser) {
		Integer depth = 0;
		do {
			System.JSONToken curr = parser.getCurrentToken();
			if (curr == System.JSONToken.START_OBJECT || curr == System.JSONToken.START_ARRAY) {
				depth++;
			} else if (curr == System.JSONToken.END_OBJECT || curr == System.JSONToken.END_ARRAY) {
				depth--;
			}
		} while (depth > 0 && parser.nextToken() != null);
	}
	private static List<Integer> arrayOfInteger(System.JSONParser p) {
		List<Integer> res = new List<Integer>();
		if (p.getCurrentToken() == null)
			p.nextToken();
		while (p.nextToken() != System.JSONToken.END_ARRAY) {
			res.add(p.getIntegerValue());
		}
		return res;
	}
	private static List<Labels> arrayOfLabels(System.JSONParser p) {
		List<Labels> res = new List<Labels>();
		if (p.getCurrentToken() == null)
			p.nextToken();
		while (p.nextToken() != System.JSONToken.END_ARRAY) {
			res.add(new Labels(p));
		}
		return res;
	}
	private static List<Stories> arrayOfStories(System.JSONParser p) {
		List<Stories> res = new List<Stories>();
		if (p.getCurrentToken() == null)
			p.nextToken();
		while (p.nextToken() != System.JSONToken.END_ARRAY) {
			res.add(new Stories(p));
		}
		return res;
	}
	public static List<PivotalTrackerIteration> arrayOfPivotalTrackerIterations(System.JSONParser p) {
		List<PivotalTrackerIteration> res = new List<PivotalTrackerIteration>();
		if (p.getCurrentToken() == null)
			p.nextToken();
		while (p.nextToken() != System.JSONToken.END_ARRAY) {
			res.add(new PivotalTrackerIteration(p));
		}
		return res;
	}
	private static List<Stories_Z> arrayOfStories_Z(System.JSONParser p) {
		List<Stories_Z> res = new List<Stories_Z>();
		if (p.getCurrentToken() == null)
			p.nextToken();
		while (p.nextToken() != System.JSONToken.END_ARRAY) {
			res.add(new Stories_Z(p));
		}
		return res;
	}
}
```


# Last Modified


# Usage
