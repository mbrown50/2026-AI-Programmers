# AI-Powered Legacy Application Support Chatbot

## 1. Executive Summary

Large organizations often rely on internally developed legacy applications supported by a small number of Subject Matter Experts (SMEs). Critical application knowledge may be spread across SharePoint documents, user guides, support procedures, and individual employees' experience.

This proposal outlines an AI-powered support chatbot integrated with Slack. It will help employees find application guidance, follow approved troubleshooting procedures, and identify the appropriate support team when additional assistance is needed.

The solution will use the organization's existing internal Large Language Model (LLM), Retrieval-Augmented Generation (RAG), and approved internal documentation to provide application-specific support for one designated legacy application.

A key requirement is ongoing evaluation and observability. The system must measure whether it retrieves relevant information, generates accurate and useful responses, helps resolve user issues, and escalates unresolved requests appropriately. These measurements will help SMEs identify knowledge gaps and improve the system over time.

## 2. Problem and Current Workflow

- Application knowledge is often held by a small group of SMEs or spread across multiple documentation sources.
- Users may not know where to find application guidance or which team to contact when issues occur.
- Support requests are frequently sent through informal channels such as Slack, email, direct messages, or calls.
- General IT help desks may not have the application-specific knowledge required to resolve these issues.
- SMEs spend time answering repetitive questions instead of focusing on more complex application issues.
- Existing documentation may be incomplete, outdated, or difficult to locate.

The proposed solution aims to make approved application knowledge easier to access while improving the consistency and measurement of the support process.

## 3. Proposed AI-Powered Solution

Develop a dedicated AI chatbot within Slack to provide first-level support for one designated legacy application.

The chatbot will:

- Use the company's existing internal LLM with application-specific instructions and guardrails.
- Retrieve relevant information from approved documentation using RAG.
- Generate responses grounded in retrieved information and include source references.
- Identify questions outside its defined scope or beyond the available knowledge.
- Ask clarifying questions when additional information is needed.
- Guide users through approved troubleshooting procedures.
- Direct unresolved issues to the appropriate support process.
- Collect feedback and provide performance information for ongoing evaluation.

The chatbot will supplement existing IT help desk and application support teams, not replace them. Human support will remain available for complex, sensitive, or unresolved issues.

## 4. Target Users and Use Cases

### Primary users

- Business users who rely on the designated application.
- Store Planners and other employees who need application guidance.
- Application support personnel and technical SMEs.

### Example use cases

- Finding instructions for using an application feature.
- Understanding common application errors.
- Getting guidance on application access and connectivity.
- Finding the correct support contact.
- Following approved basic troubleshooting procedures.
- Preparing a structured support request when an issue cannot be resolved.

## 5. Core Features and User Flow

### Slack chatbot interface

- Users interact with the chatbot through a designated Slack channel or direct message.
- The chatbot identifies the application-support context and asks clarifying questions when necessary.

### Knowledge retrieval and responses

- Searches approved documentation for relevant information.
- Provides answers grounded in retrieved content.
- Includes source references and, where available, document update or validation dates.
- Explains when information is unavailable or insufficient to provide a reliable answer.

### Basic troubleshooting

- Provides approved instructions for common application issues.
- Examples include application launch guidance, access instructions, and VPN or network checks.
- Destructive actions and changes to production systems are excluded from the initial release.

### Support escalation

- Gathers relevant details when an issue cannot be resolved.
- Identifies the appropriate support category.
- Directs users to the correct ticketing process or monitored support channel.
- Where authorized integrations exist, creates or prepopulates a support ticket and notifies the appropriate Slack channel.

## 6. AI Capabilities

### Large Language Model (LLM)

- Uses the company's existing internal LLM for natural-language understanding and response generation.
- Applies application-specific system instructions to keep responses within the chatbot's defined scope.
- Interprets user questions and asks for clarification when necessary.
- Avoids generating unsupported technical instructions.

### Retrieval-Augmented Generation (RAG)

- Retrieves relevant content from approved internal documentation.
- Uses an embedding model to convert document content and user queries into numerical representations.
- Uses a vector database for semantic search, potentially combined with keyword search.
- Returns relevant document sections and metadata to the LLM.
- Grounds generated responses in retrieved information and provides source references.

### Knowledge management

- Approved documentation remains the source of truth for application information.
- Document owners are responsible for reviewing and updating source material.
- Updated documents are reprocessed and reindexed by the retrieval pipeline.
- Outdated, conflicting, or unverified information should be flagged rather than presented as confirmed guidance.

### Response confidence and escalation

- Recognizes when retrieved information is insufficient to answer a question reliably.
- Requests clarification or escalates to human support when necessary.
- Communicates limitations rather than filling knowledge gaps with assumptions.

## 7. Data, Inputs, Tools, and Integrations

### Data sources

- SharePoint application documentation.
- Application user guides and FAQs.
- Approved technical support procedures.
- Validated historical support resolutions.
- Approved troubleshooting instructions.

### Required technologies and integrations

- **Slack:** User interface for chatbot interactions.
- **Internal LLM:** Natural-language understanding and response generation.
- **Embedding model:** Converts documents and queries into numerical representations for retrieval.
- **Vector database:** Stores document embeddings and supports semantic search.
- **SharePoint or approved document repository:** Source of application knowledge.
- **Ticketing platform:** Jira or ServiceNow, depending on company standards.
- **Identity provider:** Authentication and access control.
- **Observability and monitoring tools:** Performance tracking, evaluation, and troubleshooting.

Model Context Protocol (MCP) could be considered if a standardized approach is needed for connecting the chatbot to approved tools and services. Any integrations should use narrowly scoped permissions.

## 8. Technical Architecture and Implementation Plan

### Proposed technical workflow

1. A user submits a question through Slack.
2. The chatbot checks whether the request is within the designated application's support scope.
3. The retrieval component processes the query and uses the embedding model to support semantic search.
4. The retrieval service searches the vector database and, where appropriate, performs keyword-based retrieval.
5. Relevant document sections and metadata are returned to the LLM.
6. The LLM generates a response using the retrieved information and application-specific instructions.
7. The chatbot returns the answer through Slack with source references and available document dates.
8. If the issue cannot be resolved, the chatbot gathers additional details and directs the request to the appropriate support process.
9. Relevant system activity and performance data are captured for monitoring and evaluation.

### Implementation phases

**Phase 1: Discovery and knowledge assessment**
- Identify the application, users, SMEs, and existing support processes.
- Identify approved documentation sources and document owners.
- Review documentation quality, completeness, and freshness.
- Define the chatbot's scope and escalation categories.

**Phase 2: RAG and chatbot development**
- Configure the internal LLM for application-specific support.
- Develop the document ingestion and retrieval pipeline.
- Configure the embedding model and vector database.
- Build the Slack chatbot interface.

**Phase 3: Support integrations**
- Integrate with the existing ticketing platform.
- Configure support categories and routing rules.
- Enable approved ticket creation and Slack notifications.

**Phase 4: Security and evaluation**
- Configure authentication, permissions, and access controls.
- Develop SME-approved test questions and expected responses.
- Evaluate retrieval quality, answer accuracy, scope limitations, and escalation.
- Validate security and data-handling controls.

**Phase 5: Pilot and continuous improvement**
- Pilot with a limited user group.
- Collect user and SME feedback.
- Monitor performance and identify recurring issues.
- Improve documentation, retrieval, prompts, and routing based on evaluation results.

## 9. Risks, Limitations, and Mitigations

- **Outdated documentation**
  - Risk: The chatbot retrieves information that no longer reflects current application processes.
  - Mitigation: Establish document owners, review dates, validation status, and a process for updating and reindexing documents.

- **Incorrect or unsupported answers**
  - Risk: The LLM generates an answer that is not supported by the knowledge base.
  - Mitigation: Use RAG grounding, source references, scope restrictions, SME testing, and escalation when evidence is insufficient.

- **Security and access**
  - Risk: Users receive information they are not authorized to access.
  - Mitigation: Use authentication, role-based access control, permission-aware retrieval, and least-privilege integration permissions.

- **Prompt injection and untrusted content**
  - Risk: User input or retrieved documents attempt to override the chatbot's instructions.
  - Mitigation: Treat retrieved content as untrusted data, maintain separate system instructions, and apply input and output guardrails.

## 10. Testing, Feedback, and Evaluation

SMEs should help establish expected answers and evaluate whether the chatbot provides accurate and useful application support.

### Ground-truth evaluation dataset

Create a test dataset containing:

- Common application questions and FAQs.
- Access and connectivity questions.
- Known application errors and troubleshooting scenarios.
- Questions outside the chatbot's defined scope.
- Questions with missing, outdated, or conflicting documentation.
- Examples requiring clarification or escalation.
- Examples involving restricted information or unauthorized requests.

### Evaluation criteria

- Does the chatbot retrieve the correct documentation?
- Are answers accurate and supported by retrieved information?
- Do responses provide enough information to help users?
- Does the chatbot recognize when it cannot answer reliably?
- Does it route unresolved issues to the correct support team?
- Does it avoid instructions outside its approved scope?

### User feedback

- Include thumbs-up and thumbs-down feedback.
- Where practical, ask whether the response resolved the user's problem.
- Review negative feedback and recurring unresolved questions.
- Allow SMEs to review flagged responses and recommend corrections.

User feedback should not automatically become approved knowledge. SMEs must validate corrections before documentation or system instructions are changed.

## 11. Observability and Ongoing Monitoring

Observability is necessary to understand how the chatbot performs across retrieval, response generation, technical operations, and user outcomes. It should provide enough traceability to identify why a response was generated and where improvements are needed.

### Retrieval monitoring

- Which documents and document sections are retrieved for each query?
- Are retrieved sources relevant to the user's question?
- Are important documents missing from retrieval results?
- Are retrieved documents current and validated?
- Are conflicting sources or low-relevance results being returned?

### Response monitoring

- Are answers grounded in retrieved documents?
- Are responses accurate when compared with SME-approved expected answers?
- Does the chatbot remain within its defined application scope?
- Does it recognize insufficient information and escalate appropriately?
- Are unsupported responses or recurring errors increasing?

### User outcome monitoring

- How many questions are resolved without human support?
- How often do users provide positive or negative feedback?
- Do users report that their problem was resolved?
- Which questions result in repeated attempts or additional support requests?
- Which issues are most frequently escalated?

### Technical performance monitoring

- Response time and model latency.
- Retrieval performance.
- Model and API errors.
- Slack and ticketing integration failures.
- Token usage and processing costs.
- System availability and reliability.

### Monitoring and improvement process

1. Capture relevant chatbot activity, retrieval results, source metadata, and user feedback.
2. Identify patterns such as unanswered questions, irrelevant retrieval results, negative feedback, and incorrect routing.
3. Flag issues for review by the appropriate SME or technical owner.
4. Determine whether the issue is caused by outdated documentation, missing knowledge, poor retrieval, incorrect instructions, or an application problem.
5. Update approved documentation, retrieval configuration, prompts, or routing rules.
6. Reindex updated documentation when required.
7. Retest the chatbot against the ground-truth evaluation dataset.
8. Monitor whether changes improve accuracy and user outcomes without introducing new issues.

**Technical traceability:** Retain relevant model and prompt versions, retrieved document identifiers and versions, document validation dates, and routing or tool actions. Logging must follow company privacy, security, and retention requirements.

## 12. Human Oversight and Escalation

The chatbot supports employees and SMEs but does not replace application support expertise.

- SMEs define approved application knowledge and expected answers.
- Documentation owners maintain source information.
- Humans review flagged responses and approve knowledge corrections.
- Support teams investigate issues requiring application-specific expertise.
- Access approvals and production changes remain subject to existing human approval processes.
- Complex, sensitive, or uncertain issues are escalated rather than handled autonomously.

## 13. Success Criteria

The pilot should establish baseline measurements and compare results after implementation.

### Operational measures

- Reduction in repetitive questions received by SMEs.
- Reduction in time spent locating application documentation.
- Increase in questions resolved through approved self-service guidance.
- Reduction in unnecessary or incorrectly routed support requests.

### AI performance measures

- Retrieval relevance and accuracy.
- Percentage of answers supported by approved documentation.
- Accuracy against SME-approved evaluation questions.
- Correct identification of out-of-scope questions.
- Correct escalation and routing rates.

### User experience measures

- User satisfaction and feedback.
- Percentage of users reporting that their issue was resolved.
- Reduction in repeated questions and follow-up requests.
- Time taken to create a complete support ticket.

### Knowledge-management measures

- Percentage of important documents with identified owners.
- Percentage of documents reviewed or validated within the required period.
- Number of missing, outdated, or conflicting documents identified.
- Reduction in recurring questions caused by documentation gaps.

## 14. Future Improvements and Expansion

Once the initial chatbot demonstrates reliable performance, additional capabilities could be considered:

- Expand support to other legacy applications.
- Introduce MCP integrations to connect with additional approved internal tools and services.
- Explore AI agents for routine support tasks, with defined permissions and human oversight.
- Integrate approved application availability checks.
- Identify recurring application problems and knowledge gaps across support requests.
- Automate selected support workflows where appropriate.

Any future automation involving production systems, sensitive data, or significant business impact should require appropriate validation, access controls, and human approval.
