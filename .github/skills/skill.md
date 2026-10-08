# Skill: Markdown Plain-Text to EndNote Temporary Citation Converter

## Overview
This skill converts plain-text academic citations inside a Markdown document into standardized **EndNote Temporary Citations** (e.g., `{Author, Year}`). It automates database lookups via PubMed to verify the source metadata, formatting the text so that the user can seamlessly import it into Microsoft Word and activate live citations using the EndNote plugin.

## AI Execution Workflow

### Step 1: Parsing & Text Extraction
1. Scan the incoming Markdown manuscript to identify all plain-text in-text citations. 
2. Identify common variations:
   - Parenthetical: `(Smith et al., 2020)`, `(Jones & Baker, 2019)`
   - Narrative: `Smith (2020) demonstrated...`
   - Multi-citation groups: `(Alpha, 2018; Beta, 2021)`
3. Extract core metadata fields: **Lead Author Last Name**, **Publication Year**, and nearby contextual keywords if the citation style includes them.

### Step 2: External Metadata Verification (PubMed Search)
1. Treat each identified citation as a query profile.
2. Formulate an optimized search query using the extracted primary author and year (e.g., `Smith [AU] AND 2020 [DP]`).
3. Cross-reference the resulting titles or abstracts with the contextual sentence from the document to verify the correct entry.
4. Retrieve the primary author's exact cataloged last name and publication year to construct the temporary citation.

### Step 3: Syntax Transformation & Conversion
1. Replace the native inline text citations strictly with EndNote's required unformatted temporary citation syntax: `{Author, Year}`.
2. For narrative citations, keep the author outside the brackets but place the unformatted placeholder cleanly: `Smith {Smith, 2020}`.
3. Separate multi-source arrays using semicolons within a single bracket set or sequential bracket blocks depending on user preferences, defaulting to: `{Alpha, 2018; Beta, 2021}`.
4. **Safety Constraint:** Do not alter, strip, or break any markdown syntax, code blocks, math formulas, headers, or structural layouts surrounding the citations.

### Step 4: Exception Log Generation
At the very end of the modified document, append an **Automated Warning List**. This section must catch cases where manual human intervention is required. Flags include:
- **[AMBIGUOUS]:** Multiple distinct papers match the same `Author, Year` criteria on PubMed.
- **[NOT_FOUND]:** No authoritative entry matches the author and year combo on PubMed.
- **[MALFORMED]:** In-text citations missing critical metadata components (e.g., missing a year).

---

## User Instructions (The Human Role)
Once the AI returns the modified Markdown file, follow these precise manual steps to finalize your live EndNote bibliography:
1. **Export the Document:** Convert or copy this generated Markdown text into a Microsoft Word file (`.docx`). You can use a tool like Pandoc or paste the text directly into Word.
2. **Open EndNote:** Ensure your target EndNote Library is open on your desktop.
3. **Trigger the Add-In:** Inside Microsoft Word, navigate to the **EndNote toolbar tab** on the top ribbon.
4. **Compile Live Citations:** Click the **"Update Citations and Bibliography"** command. EndNote will automatically scan your text for the `{Author, Year}` wrappers, prompt you to resolve any flagged ambiguous entries, and compile your final dynamic bibliography perfectly.

---

## Output Template Structure

Return your output following this format:

```markdown
# [Manuscript Title or Updated Document]

[Body text containing updated {Author, Year} citations...]

***

## ⚠️ Automated EndNote Conversion Warning List
The following citations require manual verification before or during your EndNote library update:

* **[AMBIGUOUS]** Line {line_number}: `(Smith, 2020)` matched multiple entries on PubMed. EndNote will prompt you to select the correct record.
* **[NOT_FOUND]** Line {line_number}: `(Unknown, 2025)` yielded zero hits on PubMed. Please check spelling or verify your library record.
```