# Literal Code Search using Sourcegraph


### Live Application 1

**Sam** is a new hire at Sourcegraph, He is currently in his second week of onboarding as a Mid-Level Software developer with the Front-end Team. A part of his week 2 task is to get familiar with the `package.json `files in the repo within the next two days.Sam doesn’t know where the server folder is located in the Sourcegraph Repository. How can Sam get up to speed in the shortest possible time?!

### Search Query:
`repo:^github\.com/sourcegraph/sourcegraph$ file:package.json count:all`

[Results in Sourcegraph
](https://sourcegraph.com/search?q=context:global+repo:%5Egithub%5C.com/sourcegraph/sourcegraph%24+file:package.json+count:all&patternType=literal)
