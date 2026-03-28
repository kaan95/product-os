# Create Documentation

Generate comprehensive documentation for business logic, processes, or workflows and save it to the appropriate documentation folder.

$ARGUMENTS

## Arguments

The user must provide the following arguments:

- **Category** (required): The category for the documentation. Options: finance, tv, rsv, lawyers, post, general
  - `finance` - Financial processes (invoicing, payments, DATEV, accounting)
  - `tv` - TV/Rechtsschutz insurance related processes
  - `rsv` - RSV insurance related processes
  - `lawyers` - Lawyer workflows and processes
  - `post` - Postal/mail related processes
  - `general` - General documentation not fitting other categories

- **Title** (required): The title/topic of the documentation

## Instructions

1. Always write the documentation in English.
2. Create a comprehensive markdown document covering the logic, process, or workflow described by the user.
3. Save the document to `/documentation/{category}/{sanitized-title}.md` where:
   - `{category}` is the category argument (finance, tv, rsv, lawyers, post, or general)
   - `{sanitized-title}` is the title converted to lowercase with spaces/special chars replaced by hyphens
4. If the user provides information from meetings, Notion pages, or other sources, incorporate that information into the documentation.
5. Structure the documentation clearly with appropriate sections.
6. Include relevant details about business rules, edge cases, technical considerations, and any dependencies.

## Documentation Structure

The generated documentation should include the following sections (adjust as needed based on content):

1. **Title**: Clear, descriptive title
2. **Metadata**: Category, creation date, last updated date
3. **Overview**: Brief description of what the document covers
4. **Purpose**: Why this documentation exists and who it's for
5. **Key Concepts**: Important terms or concepts to understand
6. **Logic/Process Flow**: Detailed explanation with step-by-step breakdown
7. **Business Rules**: Any business rules, constraints, or conditions
8. **Configuration**: Configuration details, parameters, or settings (if applicable)
9. **Examples**: Concrete examples or use cases
10. **Edge Cases**: Special cases or exceptions to handle
11. **Dependencies**: Related systems, data, or other dependencies
12. **Technical Notes**: Technical implementation details (if applicable)
13. **References**: Links to related documentation, Notion pages, Jira tickets, or code
14. **Questions/Open Items**: Any unresolved questions or items for follow-up

## Output

After creating the documentation:

1. Confirm the file path where the documentation was saved
2. Provide a brief summary of what was documented
3. Show the file path as a clickable link in the format: [filename.md](documentation/category/filename.md)
