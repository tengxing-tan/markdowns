Final security review

view password/client secret as text
- Only retrieve passwords when user click the button. *lazy initialization*
- Keep audit logs for every retrieval of the passwords.
- Show that same audit logs for customer review?
- Discussed with security experts?

I thought this might help with preparing and documenting for FSR:

1. Solution diagram and related application security threats with mitigation are included in the Threat Model. 
    1. An example of a threat modeling diagram ([https://online.visual-paradigm.com/diagrams/templates/threat-model-diagram/website-threat-modeling/](https://online.visual-paradigm.com/diagrams/templates/threat-model-diagram/website-threat-modeling/ "https://online.visual-paradigm.com/diagrams/templates/threat-model-diagram/website-threat-modeling/")). The red lines are the threat boundaries.
2. Make sure all related NFRs (Application / Infra and Ops) are in “Done” or “Completed for CR” state. 
3. Ensure proper validation on the user input. This includes for example, 
    1. The hidden input fields in ASPX pages.
    2. Parsing Guid with ExactGuid.
4. Avoid including useful information like stack trace in the error message to UI. 
5. All output on the page is encoded. 
6. Avoid leaking of information by including division or identifier in the query. 
7. Ensure the input used in the filter criteria is properly handled. 
8. Ensure same Roles and rights is validated in the search page, result page and API. 
9. Beware of the manipulation of redirect URL. 
10. Proper function rights and featureset are checked. 
11. If the feature deals with sensitive data, make sure the retrieval of the sensitive data with the roles and rights checking. 
12. Security tests are performed and documented.