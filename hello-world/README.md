# hello-world

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).


### Setup instructions
```
yarn -i
yarn serve
```


indexPrizeWinArr: [0, 4, 5, 7],

### Brief explanation of your solution.

We have 9 segments in the wheel. So we have degrees rer segment: 360/9 = 40 degrees
 Step1: When we click to play button, we have number rounds * 360 and generate number random in range 0 -> 360
Then 360/ number random( in step1) 
let degreesPerSegment = 360/9 = 40


case1: (ex: degrees random = 10, we can see 10/degreesPerSegment = 0.25), after that we have number 0. => index =  9 - 0 = 9
case2: (ex: degrees random = 50, we can see 50/degreesPerSegment = 1.25), after that we have number 1. => index =  9 - 1 = 8
case3: (ex: degrees random = 150, we can see 150/degreesPerSegment = 3.75), after that we have number 3. => index =  9 - 3 = 6

define const indexPrizeWin = any number in range 0 -> 9
if index == indexPrizeWin => win
if index != indexPrizeWin => not win

