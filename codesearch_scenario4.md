# Regex Code Search using Sourcegraph


### Live Application 4

To match RGB hex color codes, we can write a regular expression that has three parts:

- A hash symbol **(#)**

- A character class for hexadecimal characters: **[0-9a-f]**

- A repetition operator, indicating that we're looking for 6 characters that match the above character class: **{6}**

### Search Query:
`#[0-9a-f]{6} lang:css  `

[Results in Sourcegraph
](https://sourcegraph.com/search?q=%23%5B0-9a-f%5D%7B6%7D+lang%3Acss+patternType%3Aregexp&_ga=2.88360859.122222794.1636971533-378149307.1627890958)