# Variables in integration settings

When you set up integration of your form with other services, you can send responses or other data from the form to the service. For example, you can insert the user's responses into the text of an email or insert data into issue fields in {{ tracker-short-name }}.

Use variables to do this:

1. In the **Integration** tab of your form, [add an action](notifications.md#add-integration).

1. Select the field and click ![](../_assets/forms/add-var.png) to the right.

1. Select a variable from the list to add to the field.

1. If you're using variables like <q>Prompt response</q> or <q>Response ID</q>, you can choose a [filter](#var-filters) for variable values if needed.

1. Click **Save**.

When data is sent to the service, the variable is automatically converted to a value: a response to a prompt, test result, or technical data.

{% note warning %}

When [integrating your form with {{ tracker-short-name }}](create-task.md), you can add the employee who's specified in a response to the <q>People</q>, to the **Reporter**, **Assignee**, and **Followers** fields in Tracker. To do so, add a **Response ID** variable to the field. If you use a **Response to prompt** variable, integration won't work.

{% endnote %}

> See below sample text of an email containing all the user's responses to the form prompts.
>
> ![](../_assets/forms/variables-example-new.png)

## Filters {#var-filters}

If integration settings contain prompt responses added using variables, errors may occur if responses do not match the format required for integration. For example, if you add a response to the <q>Long text</q> prompt to the HTTP request body and this response contains line breaks, integration won't work.

To avoid data format errors, use the following filters for variables:

* **Sanitize string** to remove special characters from the text of a response.

* **JSON** to convert the response text to a JSON-compatible format.


![](../_assets/forms/var-filter-json.png)

## Formatting of responses {#formatting-responses}

If the integration settings contain question responses added using variables, you can select the format of responses submitted from the form.

* **Plain text** shows the data in the "question - response" format.

* **Formatted** wraps questions and responses in a code block.

* **JSON** shows responses in the `"key": "value"` format.

## Variable reference {#section_wqx_1j2_p2b}

You can use the following variables in action settings:

| Variable | Description |
----- | -----
| **User data** | Personal data of the user who filled out the form<br/><br/><br/>Variables from this group are only converted to the user's personal data if the form is created in [{{ forms-full-name }} for business](forms-for-org.md) and the user who filled out the form is an employee of the organization. You can only get data from external users if they provide their data in response to the form prompts. |
| Name | Username |
| Login | Username of the user |
| Email | The user's email |
| Gender | The user's gender |
| Department | The employee's department (for users of [{{ forms-full-name }} for business](forms-for-org.md)) |
| Phone | The employee's work phone number (for users of [{{ forms-full-name }} for business](forms-for-org.md)) |
| Supervisor | The employee's direct supervisor (for users of [{{ forms-full-name }} for business](forms-for-org.md)) |
| Team | Teams the employee is a member of (for users of [{{ forms-full-name }} for business](forms-for-org.md)) |
| **Data from the organization** | Information from the organization's address book in [{{ org-full-name }}]({{ link-org-main }}) |
| User information | A field from the card of the employee who filled out the form |
| Information from a response to a prompt | For prompts of the **People**, **Departments**, and **Teams** type, it's a field from the card of an employee or department specified in the response.  |
| **Test results** | The user's result in a [test or quiz](tests.md) |
| Maximum test points | The maximum number of points that can be scored in the test |
| Total prompts with points | The number of prompts for which the user can get points |
| Points scored | The number of points scored by the user |
| Test results heading | [The heading of a segment](tests.md#test-result) the user's results fit in |
| Description of test results | [The description of a segment](tests.md#test-result) the user's results fit in |
| Points scored for a prompt | The number of points scored for a selected prompt |
| **Form** | The form parameters and prompt responses |
| Form ID | Unique form ID |
| Name | Form name |
| Prompt response | The user's response to a specific prompt in the form (select a prompt) |
| Responses to prompts | Multiple-choice responses: select the questions and set up the formatting for responses |
| Response ID | A unique ID of a completed form |
| Prompt response option ID | The unique ID of a response option for multiple-choice questions (such as <q>People</q> or <q>Drop-down list</q>). |
| Response date | The date when the form was filled out |
| Form creator's email | The email of the user who created the form |
| **Browser** | Information about the user's browser and operating system |
| OS family | Operating system type |
| OS name | Operating system name |
| OS version | Operating system version |
| Browser name | Name |
| Browser version | Version |
| **Query** | The technical parameters of an HTTP session |
| Host | The user's computer name |
| URL | Form address |
| All GET parameters | The values of all request parameters.<br/><br/>Learn more about how to [use GET parameters to pre-fill a form](get-params.md). |
| GET parameter | The value of a specific request parameter (enter the parameter name).<br/><br/>Learn more about how to [use GET parameters to pre-fill a form](get-params.md). |
