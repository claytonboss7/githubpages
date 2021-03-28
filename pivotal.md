---
layout: default
---

## QA Sandbox Info for rrdev

Users can log into the sandbox at https://roadrebel--rrdev.my.salesforce.com by appending .sandbox_name to their Salesforce usernames. For example, if a username for a production organization is user1@acme.com, and the sandbox is named “test”, then the modified username to log into the sandbox is user1@acme.com.test.

For the QA sandbox for example my username would be admin@rr.com.rrdev
The password for this will be whatever your ccdev password was.

This sandbox will be refreshed after every deployment and has been setup to automatically pull the data it needs to work, like Conga, Community users, etc.
![alt text](https://raw.githubusercontent.com/claytonboss7/githubpages/gh-pages/assets/images/rrdevlogin.jpg "rrdev")



[back](./)
###Tracker's workflow
The following diagram illustrates Trackers workflow based on story states and Reviews.

Diagram of Trackers workflow
![alt text](https://www.pivotaltracker.com/help/kb_assets/trackers_workflow_1@1x.png "pivotal")

In the Getting Started guide, the Workflow overview article walked you through a simple workflow example. Let’s look at a more detailed example to help you tailor Tracker’s workflow to best fit your team’s needs.

A story in the life
Here’s the life cycle of a typical Tracker story:

The product owner (PO) prioritizes a story in the Backlog. Then puts a “Design” review on it so the story will be queued up in the design team’s “Design” reviews search results.
A label is added to a story and then appears in a search panel's results when filtering for that label

A designer adds the initial mock-ups to the story and sets their Design review to “Pass”.
Design Reviews passed
Design Reviews passed

The PO and designer meet with a tester and a programmer for a “three amigos”-style discovery workshop , two days in advance of an iteration planning meeting (IPM). They discuss this story, using example mapping to elicit examples of desired behavior, specify rules for the story, and document outstanding questions.
Documenting story rules, examples of desired behavior, and outstanding questions

The whole team gets together two days later for the IPM. They discuss the rules and examples for the story. The PO has the answer to the outstanding question. They talk about the dependency on the server side story, and various options for implementing it. They estimate the story at 3 points. However, as noted in the description with the story link, the story depends on a server side story that is not yet done, so the PO adds a “blocker” to the story.
A 'blocked' blocker showing in a story preview

The blocking server-side story is accepted, automatically resolving the story’s blocker. When the story is the next unstarted story in the Current panel, a developer pair starts it, which automatically assigns them as story owners. They test drive the code at the unit level, as well as with automated acceptance tests based on the story rules and examples. They explore different searches, such as using regular expressions, and consult with the tester and PO as new questions come up. They click the Finish button, but feel the story needs more exploratory testing, and that they should double-check design implementation, so they add the “Test (QA)” and “Design” Reviews to it.
Reviews on stories

When the CI build for the story’s code passes, the artifacts are automatically deployed to a test environment. The tester verifies this, and clicks the Deliver button. The tester pairs with the designer to verify the look and feel of the search. The designer is satisfied with the results and sets the “Design” review to “Pass”. After more exploratory testing, the tester identifies two minor issues that are outside the scope of the story. They add new stories for these in the “shopping” epic. Satisfied that the story provides the right value for users, the tester sets the “Test (QA)” review to “Pass”, and adds a “Product Owner (PO)” review so that the PO notices the story is ready for them to do final acceptance.
Reviews on stories

Note: The My Work panel will show all stories in Delivered status (i.e., ready for to be accepted or rejected) for which you are the requester, so you can easily see which are ready to accept.
The PO notices a cosmetic issue, but it’s not something that has to be fixed before the beta release. They create another story in the “shopping” epic to address it later, rather than reject the story. They accept the story, which moves up into the green accepted stories at the top of the Current panel.
Accepted story in current
How is your team doing?
All stories are not created equal. Straightforward ones may be accepted within hours of being started. With more complicated ones, we may find that some rules were missed or the feature can’t quite be implemented as designed after all. Clicking that Reject button may sound harsh, but it just means there’s a bit more to be done, and iterating a few times is sometimes necessary. When rejecting a story, add comments with details about why it was rejected, including screenshots and any other useful information.

Keep tabs on story cycle time and rejection rate by checking the Cycle time report in the Analytics section of Tracker. Your team can use this information to identify problem areas and try experiments to shorten cycle time and reduce rejection rate.

Watch the Cumulative Flow chart to see story states by day during the iteration. This helps identify problem areas such as falling into a “mini waterfall” scenario, with no stories being completed until the end of the iteration.

Need more control over planning the current iteration?
Tracker provides a way to let you manually plan the current iteration. Check out the Automatic vs. Manual Planning section in Using Projects.

Tips for handling bugs
As noted in the Getting Started article on Tracker’s workflow, bug stories follow the same workflow as feature stories. However, bugs sometimes follow different paths. You may want to preserve the information in a bug story, even if the team isn’t going to do any work specifically on that story.

Your team may decide not to fix a particular bug. When this happens, teams typically mark the bug story accepted, and tag it with an appropriate label, such as “wont fix.” It’s always helpful to add a comment describing the reason.

An issue reported as a bug may turn out to be a missing feature, or it could be expected behavior. You might prefer to change the story type from bug to feature. Or, you could tag it with a “not a bug” label and change the state to Accepted.

While fixing bugs as soon as possible is a good practice, sometimes a bug story may linger long enough that it is fixed by a different story. An option is to comment on what was tried then tag it with a “not reproducible” label and change the state to accepted.

Tips for using Chores and Releases
Chores are stories that are necessary but provide no direct, obvious value to the customer (e.g., “Update SSL Certs”). Because they don’t typically require extra validation when they’re finished, the states for chores are just unscheduled (when in the Icebox), unstarted, started, and accepted.

Releases are milestone markers that allow your team to track progress toward concrete goals (e.g., stakeholder or investor demos, software launches, etc.). It’s possible to specify target dates for releases. All stories for a milestone or release should go above the marker for it. Releases are automatically placed in the started state upon being created or dragged in the Backlog, and also have the unscheduled (when in the Icebox) and accepted states. For more please see Organizing releases.