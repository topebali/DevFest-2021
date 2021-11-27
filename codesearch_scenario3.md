# Structural Code Search using Sourcegraph


### Live Application 3

Suppose we're investigating a bug that only happens when an array, parts, is empty. We're looking for if statements where the condition starts with a check for whether the array is empty. 


### Search Query:
`fprintf(stderr, ...) lang:c repo:^github\.com/torvalds/linux$`

[Results in Sourcegraph
](https://sourcegraph.com/search?q=fprintf%28stderr%2C+...%29+lang%3Ac+repo%3A%5Egithub%5C.com%2Ftorvalds%2Flinux%24+patternType%3Astructural&_ga=2.60181037.122222794.1636971533-378149307.1627890958)

In the results, we'll find code blocks that get executed when that particular array is empty, which might bring us closer to finding the cause of the bug that we're investigating.