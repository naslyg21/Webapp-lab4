## Part 1: Run the Application

I opened the Peer Tutoring Hub application in GitHub Codespaces and submitted a valid tutoring request using request-form.php. I selected course IS 6465, chose Exam review and Practice problems, and entered a reason for requesting tutoring. After submitting the form, the application redirected me to process-request.php and displayed a confirmation message stating "Request received." It showed my course, request details, selected topics, and a status of "Pending review." This confirmed that my request was accepted.

![Tutoring request confirmation](Screenshots/Screenshot%202026-11-01%20230655.png)

## Part 2: Shared PHP Templates

**1. What does header.php provide?**

The `header.php` file provides the basic HTML structure, including the document type, language, character encoding, viewport settings, page title, and CSS links.

**2. Where is the shared CSS file linked?**

The shared CSS file is linked in `includes/header.php` using `<link rel="stylesheet" href="css/styles.css">`. The header also loads Bootstrap 5.3.3.

**3. What does nav.php provide?**

The `nav.php` file creates the navigation bar with links to the homepage (`index.php`), the requests page (`requests.php`), and the tutoring request form (`request-form.php`).

**4. What does footer.php provide?**

The `footer.php` file displays the Peer Tutoring Hub footer, loads the Bootstrap JavaScript bundle, and closes the HTML body and document.

**5. What is the benefit of using shared templates?**

Shared templates reduce duplicate code and keep the website consistent. If a developer needs to update the navigation, header, or footer, they can modify one shared file instead of updating every page individually.

## Part 3: Form Controls

**1. Dropdown menu (`select`)**

The course dropdown allows users to select one course from IS 6465, IS 6495, or IS 6570. The `required` attribute ensures a course must be selected.

**2. Date input (`type="date"`)**

The preferred date field allows users to select a date for their tutoring session. It uses the `required` attribute to prevent an empty submission.

**3. Textarea (`textarea`)**

The reason field allows users to describe what they need help with. It uses `required` and `maxlength="500"` to require an answer and limit the text to 500 characters.

**4. Checkboxes (`type="checkbox"`)**

The topics checkboxes allow users to select multiple options: Exam review, Practice problems, and Study plan. They use `name="topics[]"` so PHP can receive multiple selected values as an array.

**5. Radio buttons (`type="radio"`)**

The preferred time radio buttons allow users to select only one option: Morning, Afternoon, or Evening. They share the name `preferredtime`, making them part of the same group.

**6. Hidden input (`type="hidden"`)**

The hidden input sends `form_name="tutoring_request"` with the form submission without displaying a field to the user.

**7. Submit button (`type="submit"`)**

The Request session button submits the form data to `process-request.php` using the POST method.

## Part 4: Validation Tests

**Test 1: No topics selected**

- Input: Submitted a request without selecting any tutoring topics.
- Expected result: The application should reject the submission.
- Actual result: The application displayed "Select at least one valid topic."
- Result: PASS

**Test 2: Description too short**

- Input: Entered "Help" in the description field (4 characters).
- Expected result: The application should reject descriptions shorter than 10 characters.
- Actual result: The application displayed "Describe your request using 10 to 500 characters."
- Result: PASS

**Test 3: Valid request**

- Input: Selected IS 6465, Exam review and Practice problems, Evening, and entered a valid description.
- Expected result: The application should accept the request.
- Actual result: The application displayed "Request received" with a status of "Pending review."
- Result: PASS

**Conclusion:** The validation functions correctly rejected invalid submissions and accepted a valid tutoring request.

### Read Operation – request-details.php

The request-details.php file retrieves a request ID using the GET method and validates it with FILTER_VALIDATE_INT. It searches an array for the matching request and displays its information. The file also uses htmlspecialchars() to safely display data and provides links to edit or cancel the request.

### Update Operation – edit-request.php

The edit-request.php file displays a form populated with existing tutoring request information. It uses a PHP array to store sample data and htmlspecialchars() to safely display values. The form allows users to modify the course, request description, preferred date, topics, and preferred time. It uses POST to submit changes and includes Save changes and Cancel buttons.

### Delete Operation – delete-request.php

The delete-request.php file retrieves and validates a request ID using the GET method and FILTER_VALIDATE_INT. It displays a confirmation page allowing users to cancel or keep a tutoring request. The confirmation form uses POST to submit the cancellation, while the Keep request link returns to the request details. The current starter code does not implement permanent deletion.