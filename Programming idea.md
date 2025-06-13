# Circulation dependency
question: given items & dependencies, check if circular relation
```js
// input
// no circular
itemIds = [1,2]; dependencies = [0,1]; // 1-2
itemIds = [1,2,3]; dependencies = [0,0,0]; // none ❎ does not solved below
itemIds = [1,2,3,4]; dependencies = [0,1,0,3]; // 1-2 3-4 

// circular
itemIds = [1,2]; dependencies = [2,1]; // 1-2-1; 1 exists open & end
itemIds = [1,2,3]; dependencies = [2,3,1]; // 1-2-3-1
itemIds = [1,2,3,4]; dependencies = [4,1,2,3]; // 1-4-3-2-1
```

answer
```js
function isCircular(items, dependency) {
    // if (isMismatchLengthOrNoList &&
	//    isDisconnectedGraph &&
	//    isAnySelfLoop &&
	//    isInvalidDependency) {
	//	return false;    
	// }
	const individualNodes = items.filter((e, i) => !dependency[i]);
	return !hasRootNodes(individualNodes, dependency);
}

function hasRootNodes(individuals, dependency) {
	const root = individuals.filter(node => dependency.includes(node))
	return root.length > 0;
}

const output = isCircular([1,2,3,4], [4,1,2,3]); // true
console.log(output)
```

> Common method is to use **graph traversal algorithms** like Depth-First Search (DFS) or Breadth-First Search (BFS) to detect cycles more efficiently.


