# Code Formatting Guideline
Formatting code in a uniform manner greatly increases development speed.

Formatting code manually requires a second look on the code written by developers, increasing code quality. Automatic formatting tools lack the ingenuity to properly group code, check naming and handle exceptions.

§1 Source code should be as platform and developer independent as possible. 
Indentation should be done with `\t`, as it represents an actual tab. It can be configured to each developers preferred width. The guidelines should never lead to a situation, where spacing out of tabs or single spaces would be required.

This is not and *cannot* be a definitive formatting rule book.

## Core Principles
- prefer explicit over implicit statements
- keep space, but don't force constant scrolling
- uniformity over cool coding tricks
- kiss

Do not comment out unused code. We have version control. If a section of code might have to be introduced back later on, leave a note instead.
Remove any debugging comments.

## Control Statements
If conditions should be formatted with a space before and after the condition, the else should be on the same line as the closing bracket.
```
// optional comment explaining why this statement is required
if (condition) { 
	// optional (multiline) comment explaining why the code reached this location (elaborating on the condition)

	...
} else if (condition) {
	// optional comment
} else {
	// optional comment
}
```

The block brackets (`{}`) are **required**. Never omit the block brackets in control statements, as issues will occur with future changes.

The use of `do while` is discouraged. Use the control structure `for of` instead of the array function (`forEach`). Is your `.map? really a `.map` or a lazy for?

Loops should follow the same style
```
// optional comment
for (let variable of iterator) {
	...
}

// optional comment
while (condition) {
	...
}
```

Switches should be avoided whenever possible, as most use cases stem from architecture issues, for example using a 'type' column instead of properly splitting the types into separate classes. 

Switches should only be used when writing protocols (with multiple serialized message-types), command line interfaces (for switching between arguments) or keyboard input handling.

Adding a block (`{}`) around a case greatly increases its readability and is required.
```
switch (input) {
	case option:
	case option: {
		...

		break;
	}

	default: {

	}
}
```

Classes are defined with the same indent:
```
class Locomotive extends Vehicle {
	...
}
```

## Breaking 
Code should be split into multiple lines when the readability suffers. 

Split chained actions, split complex conditions - operator first
```
await this.db.locomotives
	.where(
		locomotive.uicIdentifier.startsWith(uicGroup)
		|| locomotive.age > this.minMaintenanceAge
		|| (
			locomotive.maintenanceDate.isToday()
			&& locomotive.age < 50
		)
	)
	.orderBy(locomotive => locomotive.name)
	.toArray()
```

Complex math operations should always have a comment. Split the expression into multiple statements or keep the expression readable by adding spaces.
```
// calculates the distance traveled by the train
// subtracts the drag coefficient from all cars in the train
let distance = (
	this.speed - (
		this.pullCoefficient - this.cars.reduce(
			(sum, car) => sum + car.dragCoefficient, 0
		)
	)
) * (lastFrame - now) / 1000;
```

Break HTML attributes when lines get long
```
<ui-field>
	<input
		id={this.fieldId}
		validate={this.validator}
		$ui-value={this.value}
	/>

	<label for={this.fieldId}>
		{this.label}
	</label>
</ui-field>
```

## Ordering
Ordering class makes finding code quicker
```
class ClassName {
	static shared: ClassName; // shared singletons / globals

	static name = value;
	private static name = value; 

	name = value;
	private name = value; 

	static name(parameter: type, ...spread: type[]) {
		...
	}

	private static name(parameter: type, ...spread: type[]) {
		...
	}

	constructor() {

	}

	name(parameter: type, ...spread: type[]) {
		...
	}
}
```

Large static lists, for example a list of all colors by name in a `Color` class should be located at the bottom, as they will rarely be updated and only lead to unnecessary scrolling. The developer will find the items quickly when scrolling down.

## Grouping
Spacing should be used to group code.
Groups can be commented above, items within a group may be commentated inline.

```
class Locomotive {
	// identifying properties
	name: string;
	uicIdentifier: string;

	// force properties
	weight: number;
	pullStrength: number;

	// electrical power properties
	startupAmperage: number;
	powerCoefficient: number;

	reset() {
		this.name = '';
		this.uicIdentifier = '000-00-000-AA';

		this.weight = 0;
		this.pullStrength = 0;

		this.startupAmperage = 0;
		this.powerCoefficient = 1; // a power coefficient of one indicates no power usage
	}
}
```

## Naming
Names should be as descriptive as possible. We'd rather have a too long name than a too short name - we have autocompletion anyways, we are not programming on notepad.

Rename any variable or property whenever the name is no longer fit. There is automatic renaming, it only takes seconds.

We use camelCase whenever possible, but some languages, like python prefer the use of snake_case. 

Shortening is only allowed, when every stakeholder in a project instantly recognizes it - clients and developers. For example, the project's name may be shortened. Indices in single-level `for` loops may be called `i`, or `x`, `y` and `z`, but a more descriptive name is preferred in nested loops.

Common long words, for example `min`, `max` may be shortened - but only if it is instantly recognizable. For example, `candidate` cannot be shortened into `cdt`, yes not even in a method within a `CandidateManager` where it is only used in connection with another word (`cdtCount`, ...) - just use the full name `candidateCount` - or maybe, if it can't be mistaken for another count, only use `count`.

If multiple properties seem to have the same prefix, it may be more suitable to move them to a separate class or combine them into a object.

The following names should never be used in a model and should be avoided in code:
- value
- item
- amount
- object
- instance
- type

A table named `item` is not descriptive. What `item` do you mean, is it referring to a product in a e-shop database? - use `product`! An item in a shopping cart? - use `cart_item`. 

This code sums up the price of all products. This took a second to figure out.
```
let value = 0;

for (let item of await db.product.toArray()) {
	value += item.price;
}
```

The following is preferred, as this is instantly recognizable.
```
let priceSum = 0;

for (let product of await db.product.toArray()) {
	priceSum += product.price;
}
```

## File Size
Classes should be split when they reach a unmanageable size. A developer should not have to constantly scroll to reach code. But a class is not required for everything, as this will only increase complexity.

## Commenting
- Comment when the code is not instantly recognizable.
- Comment when a workaround had to be used.
- Comment when reading the contents of a group can be skipped with a short description.
- Create a multi line comment on more complex operations
- Comment value conversions
- Comment math expressions
- Document Protocols

## Example Exceptions
Irregular array breaking to ease the readability of parameters and their values 
```
spawn([
	'git', 'commit',
	'-m', this.message
])
```