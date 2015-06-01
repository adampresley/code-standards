ColdFusion Best Practices
========================

**Author:** Adam Presley

1. Scoping
----------
Scoping in ColdFusion defines the context in which variables are valid. There
are a few rules and gotcha's for scoping in ColdFusion which will be outlined
here.

* *All* variables in components (CFC) must be prefixed with a scope
* Any variable in a CFM file must be prefixed with a scope, *except* those
   intended for the **variables** scope.
   - This is the default scope for CFM pages
   - Not prefixing here does no harm

In this example we'll see a CFC and CFM page using scopes correctly.

**Example CFC**
```js
component output="false" {
   this.OT_MULTIPLIER = 1.5;
   this.HOURS_PER_WEEK = 40;

   public PayService function init() output="false" {
      variables.otCalculatorService = new OTCalculatorService(
         hoursPerWeek=this.HOURS_PER_WEEK
      );

      return this;
   }

   public numeric function calculateWeeklyPay(
         required Employee employeeRecord,
         required numeric hoursWorked
   ) {
      local.otHours = variables.otCalculatorService.determineOTHours(
         hoursWorked=arguments.hoursWorked
      );
      local.regularHours = arguments.hoursWorked - otHours;

      local.regularPay = calculateRegularPay(
         employeeRecord=arguments.employeeRecord,
         hours=local.regularHours
      );
      local.otPay = calculateOTPay(
         employeeRecord=arguments.employeeRecord,
         hours=local.otHours
      );

      return local.regularPay + local.otPay;
   }

   public numeric function calculateRegularPay(
         required Employee employeeRecord,
         required numeric hours
   ) {
      return arguments.hours * arguments.employeeRecord.hourlySalary;
   }

   public numeric function calculateOTPay(
         required Employee employeeRecord,
         required numeric hours
   ) {
      return arguments.hours * (
         arguments.employeeRecord.hourlySalary * this.OT_MULTIPLIER
      );
   }
}
```

**Example CFM**
```cfm
<cfset paragraphStyle = request.styles.getParagraphStyle() />

<cfoutput>

<p class="#paragraphStyle#">
   Hello #session.employee.name#.<br />
   Your pay this week is #request.rc.employeePay#
</p>
```

2. Functions
------------

### 2.1 Scoping in Functions
* All variables *must be* prefixed with a scope
* Local variables *must be* declared using the form ```local.myVariable```

### 2.2 Naming
Functions perform actions. As such they should make use of verbs. Furthermore
most functions tend to operate on something, and as such should clearly call
out what they are doing and to what they are performing this action on.

**Example**
```js
public array function splitSentenceIntoWords(required string sentence) output="false" {
   return arguments.sentence.split(" ");
}
```

Notice how the verb is **split**, and we can easily see we are acting on a
sentence. That is the noun.

There are times when a simple verb may suffice. If the function is part of a
component where the intent or domain is clear, then the function name could
be shortened to reflect only what it is doing. However be cautious.
More clarity is better than assuming everyone reading your code understands
the domain.

**Example: MailProcessor.cfc**
```js
component output="false" {
   public void function process(required numeric queueID) output="false" {
      // ...
   }
}
```

### 2.3 Output
It is rare that a function should directly send output to the browser. This is
the responsibility of a view page or rendering component. Exceptions to this would
be if the function is part of a rendering component in a framework or system
that outputs contents to the browser as part of the request process.

As such all functions, unless they send content to the browser, *must* include
the output attribute set to *false*.

**Example**
```js
public void function doSomething() output="false" {
   // ...
}
```
