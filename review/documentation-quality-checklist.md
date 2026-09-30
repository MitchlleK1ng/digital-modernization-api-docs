# Documentation Quality Checklist

## Purpose

This checklist provides a standardized process for reviewing technical documentation before it is delivered to stakeholders or published for users.

The checklist is designed to help ensure that documentation is:

* Accurate.
* Complete.
* Consistent.
* Clear.
* Accessible to the intended audience.
* Aligned with project requirements.
* Free from avoidable errors.


---

## 1. Content Accuracy

Verify that the documentation accurately represents the system, process, or feature being documented.

* [ ] Technical information has been verified with the appropriate subject matter expert.
* [ ] System behavior is accurately described.
* [ ] API endpoints match the documented implementation.
* [ ] Request and response examples are accurate.
* [ ] HTTP methods are correct.
* [ ] HTTP status codes are appropriate.
* [ ] Authentication and authorization requirements are accurate.
* [ ] Configuration details are current.
* [ ] Links point to the correct documentation.
* [ ] No unsupported technical claims are included.

---

## 2. Completeness

Verify that the document contains all information required by its intended audience.

* [ ] Purpose of the document is clearly stated.
* [ ] Intended audience is identified when appropriate.
* [ ] Required procedures or workflows are documented.
* [ ] Prerequisites are documented.
* [ ] Required parameters are identified.
* [ ] Required fields are identified.
* [ ] Examples are provided where they improve understanding.
* [ ] Error conditions are documented where applicable.
* [ ] Related documentation is referenced.
* [ ] Requirements have been addressed.

---

## 3. Clarity and Readability

Verify that readers can understand the information without unnecessary effort.

* [ ] Sentences are concise and direct.
* [ ] Technical concepts are explained when necessary.
* [ ] Unnecessary jargon has been removed.
* [ ] Instructions use clear action-oriented language.
* [ ] Paragraphs focus on a single idea.
* [ ] Headings accurately describe the content that follows.
* [ ] Lists are used when they improve readability.
* [ ] Examples are easy to understand.
* [ ] Ambiguous statements have been revised.

---

## 4. Terminology and Consistency

Verify that terminology is used consistently throughout the documentation set.

* [ ] Product and system names are consistent.
* [ ] Technical terms are used consistently.
* [ ] API resource names match the documented API.
* [ ] Field names match the API specification.
* [ ] Capitalization is consistent.
* [ ] Acronyms are defined on first use when necessary.
* [ ] Similar concepts use the same terminology.
* [ ] Deprecated terminology has been removed.

### Example

If the API uses `customerId`, documentation should not refer to the same field as `customer ID`, `customer_id`, or `custId` when describing the API field itself.

---

## 5. API Documentation Review

For API documentation, verify the following:

* [ ] Base URL is correct.
* [ ] API version is documented.
* [ ] HTTP methods are correct.
* [ ] Endpoint paths are correct.
* [ ] Path parameters are documented.
* [ ] Query parameters are documented.
* [ ] Request headers are documented.
* [ ] Authentication requirements are documented.
* [ ] Permissions are documented.
* [ ] Request body fields are documented.
* [ ] Response fields are documented.
* [ ] Example requests are valid.
* [ ] Example responses use valid JSON.
* [ ] HTTP status codes are documented.
* [ ] Error responses are documented.
* [ ] Related API documentation is linked.

---

## 6. Visual and Formatting Review

Verify that the document follows the project's formatting conventions.

* [ ] Heading hierarchy is logical.
* [ ] Markdown syntax renders correctly.
* [ ] Tables are properly formatted.
* [ ] Code blocks use the appropriate language identifier.
* [ ] Lists are formatted consistently.
* [ ] Links are functional.
* [ ] Diagrams have descriptive labels where appropriate.
* [ ] Images have useful alternative text when applicable.
* [ ] No unnecessary formatting is used.

---

## 7. Audience Review

Verify that the documentation is appropriate for its intended readers.

### Technical Audience

For developers, system administrators, and integration teams:

* [ ] Technical requirements are sufficiently detailed.
* [ ] API behavior is clearly defined.
* [ ] Examples support implementation.
* [ ] Authentication and security requirements are documented.
* [ ] Error handling is explained.

### Non-Technical Audience

For business users, program managers, and stakeholders:

* [ ] Technical concepts are explained in plain language.
* [ ] Unnecessary implementation details are avoided.
* [ ] Business purpose is clearly communicated.
* [ ] System benefits are understandable.
* [ ] User actions are clearly described.

---

## 8. Requirements Traceability

Verify that documentation supports the documented project requirements.

* [ ] Each relevant requirement has corresponding documentation.
* [ ] Requirements are referenced consistently.
* [ ] API operations can be traced to functional requirements.
* [ ] Security requirements are reflected in technical documentation.
* [ ] Documentation requirements have been reviewed.
* [ ] Missing documentation requirements have been identified.

### Example Traceability

| Requirement                                | Documentation         |
| ------------------------------------------ | --------------------- |
| FR-001 Retrieve Customer                   | `customers.md`        |
| FR-002 Create Customer                     | `customers.md`        |
| FR-003 Update Customer                     | `customers.md`        |
| FR-004 Search Customers                    | `customers.md`        |
| FR-005 Deactivate Customer                 | `customers.md`        |
| FR-006 API Versioning                      | `versioning.md`       |
| SEC-001 Authentication                     | `authentication.md`   |
| DOC-001 API Documentation                  | API documentation set |
| DOC-002 Audience-Appropriate Documentation | `system-overview.md`  |
| DOC-003 Documentation Review               | This checklist        |

---

## 9. Security and Sensitive Information Review

Verify that documentation does not expose sensitive information.

* [ ] No real passwords are included.
* [ ] No real access tokens are included.
* [ ] No private keys are included.
* [ ] No personally identifiable information is unnecessarily exposed.
* [ ] Example credentials are clearly fictional.
* [ ] Security requirements are accurately documented.
* [ ] Sensitive information is not included in example logs.
* [ ] URLs do not contain sensitive authentication information.

---

## 10. Link and Reference Review

Verify that internal and external references work correctly.

* [ ] Internal links point to the correct files.
* [ ] API documentation links are valid.
* [ ] Requirements references are correct.
* [ ] Related-document links use the correct relative paths.
* [ ] External links, if used, point to the intended resource.
* [ ] No broken links remain before publication.

---

## 11. Final Editorial Review

Before delivery, perform a final review of the document.

* [ ] Spelling has been checked.
* [ ] Grammar has been checked.
* [ ] Punctuation is consistent.
* [ ] Capitalization is consistent.
* [ ] Sentence structure is clear.
* [ ] Repeated or unnecessary information has been removed.
* [ ] Headings accurately represent their sections.
* [ ] The document has been reviewed from the reader's perspective.

---

## Review Workflow

Documentation should move through the following review process before final delivery.

```text
Draft
  ↓
Technical Review
  ↓
Requirements Review
  ↓
Editorial Review
  ↓
Stakeholder Review
  ↓
Corrections
  ↓
Final Quality Check
  ↓
Approval / Publication
```

### Technical Review

A technical subject matter expert verifies technical accuracy.

### Requirements Review

The documentation is compared with project requirements to confirm that required information has been addressed.

### Editorial Review

The technical writer reviews clarity, grammar, structure, terminology, and consistency.

### Stakeholder Review

Appropriate stakeholders review the document to confirm that it meets the intended business or project objective.

### Final Quality Check

The documentation is checked for unresolved issues before publication or delivery.

---

## Review Record

A review record can be used to track documentation quality.

| Field             | Example       |
| ----------------- | ------------- |
| Document          | Customers API |
| Reviewer          | Technical SME |
| Review Date       | YYYY-MM-DD    |
| Review Status     | In Review     |
| Issues Identified | 0             |
| Issues Resolved   | 0             |
| Final Approval    | Pending       |

---

## Definition of Done

A document is considered ready for delivery when:

* [ ] Required content is complete.
* [ ] Technical information has been verified.
* [ ] Requirements have been addressed.
* [ ] Terminology is consistent.
* [ ] Formatting is correct.
* [ ] Links have been checked.
* [ ] Security and sensitive information review is complete.
* [ ] Editorial review is complete.
* [ ] Required stakeholders have approved the document.
