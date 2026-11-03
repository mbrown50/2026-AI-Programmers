# AI-Powered Legacy Application Support Chatbot

## 1. Executive Summary

This proposal describes an AI-powered support chatbot integrated with Slack to help employees use and troubleshoot a designated legacy business application. The chatbot will use the company’s existing internal Large Language Model (LLM) and Retrieval-Augmented Generation (RAG) to provide answers based on approved internal documentation.

The goal is to reduce time spent searching for information, improve access to support, and help employees resolve common issues. The chatbot will provide source references, recognize when information is missing or outdated, and escalate issues it cannot resolve. Human teams will retain responsibility for sensitive decisions and complex support requests.

## 2. Problem and Current Workflow

Employees currently rely on SharePoint documents, existing support resources, and internal teams for application guidance. Documentation may be difficult to locate, outdated, or inconsistent with current processes.

This creates delays, repeated support requests, and uncertainty about which instructions are correct. A chatbot could make approved information easier to find while identifying gaps that require human review.

## 3. Proposed AI-Powered Solution

Develop a Slack chatbot for one designated legacy application using:

- **Internal LLM:** Generates conversational responses using the company’s existing AI platform.
- **RAG:** Retrieves relevant information from approved SharePoint documents and internal support resources before generating an answer.
- **Knowledge management:** Tracks document owners, review dates, and update status to help identify outdated or conflicting information.
- **Human escalation:** Collects relevant details and prepares a support ticket when the issue requires further assistance.

The chatbot will answer only within its defined scope and should acknowledge when reliable information is unavailable.

## 4. Target Users and Use Cases

**Target users:** Employees who use the selected legacy application, including business users, support teams, and application administrators.

**Primary use cases:**
- Finding application instructions and process guidance.
- Understanding common errors and approved troubleshooting steps.
- Getting help with access and login procedures.
- Identifying the appropriate support team.
- Preparing support requests when an issue cannot be resolved.

## 5. Core Features and User Flow

1. An employee asks a question in Slack.
2. The chatbot identifies the request and retrieves relevant approved documentation.
3. The LLM generates an answer using the retrieved information.
4. The chatbot provides source links and document dates where available.
5. If information is missing, conflicting, outdated, or insufficient, it asks for clarification or recommends escalation.
6. When needed, it gathers relevant details and prepares a support ticket for human review.
7. The employee can provide feedback on whether the response was helpful and whether the issue was resolved.

## 6. AI Capabilities: Sample Prompts and Expected Outputs

| Sample employee prompt | Expected chatbot output |
|---|---|
| "How do I access the legacy application?" | Provides the approved access instructions, required steps, and links to relevant documentation. |
| "I'm receiving an error when submitting a report. What should I do?" | Identifies relevant troubleshooting guidance, provides approved steps, and asks for the error details if needed. |
| "How do I request access to this application?" | Explains the access request process and directs the employee to the appropriate request channel. It does not approve access. |
| "I followed the instructions, but the issue is still happening." | Asks for relevant details, summarizes the troubleshooting already completed, and prepares a support ticket for review. |
| "What is the current process for updating store information?" | Retrieves the relevant approved procedure, provides its source and last-updated date, and flags the information if its review status is uncertain. |
| "Can you give me administrator access?" | Explains the approved access request process and directs the request to the appropriate human approver. |

These examples demonstrate expected behavior rather than guaranteed responses. The chatbot must use retrieved evidence, avoid inventing instructions, and ask for clarification or escalate when necessary.

## 7. Data, Inputs, Tools, and Integrations

**Data sources:**
- Approved SharePoint documentation.
- Application user guides and troubleshooting instructions.
- Internal support procedures and approved knowledge articles.

**Tools and integrations:**
- Slack for the employee-facing interface.
- The company’s existing internal LLM.
- RAG retrieval using document chunking, embeddings, and a vector database.
- Keyword and semantic search to retrieve relevant content.
- Support ticketing integration, where available.

Retrieved information should include metadata such as document owner, source, last-updated date, and review status. Access permissions must be respected during retrieval so employees only receive information they are authorized to view.

## 8. Technical Architecture and Implementation Plan

The proposed workflow is:

1. **Document ingestion:** Collect approved documentation from selected sources.
2. **Processing:** Extract text, divide documents into meaningful sections, and generate embeddings.
3. **Indexing:** Store searchable content and metadata in a vector database.
4. **Retrieval:** Search for relevant sections based on the employee’s question.
5. **Response generation:** Provide retrieved content to the internal LLM to generate a grounded answer.
6. **Validation and escalation:** Check whether the answer is supported by the sources and whether the request requires clarification or human assistance.
7. **Monitoring:** Record relevant performance, retrieval, feedback, and escalation information.

Implementation should begin with one application and a limited set of approved documents. The pilot can then be evaluated before expanding to additional sources or applications.

## 9. Risks, Limitations, and Mitigations

| Risk | Mitigation |
|---|---|
| Outdated documentation | Assign document owners, establish review schedules, track freshness, and flag unverified content. |
| Incorrect or unsupported answers | Require source-grounded responses, test against expected answers, and allow the chatbot to abstain or escalate. |
| Unauthorized information access | Apply authentication, role-based access controls, permission-aware retrieval, and least-privilege access. |
| Prompt injection or untrusted content | Treat retrieved documents and employee input as untrusted data, separate system instructions, and apply security guardrails. |

RAG improves access to relevant information but does not guarantee that the source material is accurate or current. Documentation ownership and review processes remain essential.

## 10. Testing, Feedback, and Evaluation

Subject matter experts (SMEs) should create a ground-truth test dataset containing expected answers and appropriate escalation outcomes.

Testing should include:
- Common application questions and troubleshooting scenarios.
- Access and login requests.
- Missing, outdated, or conflicting documentation.
- Questions outside the chatbot’s scope.
- Requests involving restricted information.
- Scenarios requiring clarification or human escalation.

Evaluate the chatbot using:
- **Retrieval quality:** Does it find the correct and relevant documentation?
- **Answer accuracy:** Is the response supported by the retrieved sources?
- **Helpfulness:** Does the response help the employee solve the problem?
- **Escalation:** Does it recognize when human support is needed?
- **Security:** Does it respect access permissions and avoid exposing restricted information?

Employees should be able to provide positive or negative feedback and indicate whether their issue was resolved. Feedback should be reviewed by SMEs rather than automatically treated as approved knowledge.

## 11. Observability and Ongoing Monitoring

Monitor:
- Retrieved documents, sources, and document freshness.
- Answer accuracy, grounding, and unanswered questions.
- Model, prompt, and retrieval configuration versions.
- User feedback and issue resolution.
- Escalation frequency and recurring support topics.
- Response times, system availability, and operating costs.

Use these findings to identify knowledge gaps, outdated documentation, retrieval problems, and recurring employee needs.

## 12. Human Oversight and Escalation

Human review remains necessary for:
- Approving or changing employee access.
- Handling sensitive or restricted information.
- Resolving complex or unusual application issues.
- Approving changes to production systems and support procedures.
- Reviewing documentation updates and chatbot feedback.

The chatbot can guide employees through approved processes and prepare support tickets, but it should not independently approve access or make sensitive business decisions.

## 13. Success Criteria

The pilot should measure:

- **Efficiency:** Reduced time spent searching for information and handling common support questions.
- **AI performance:** Accurate, relevant, source-supported answers and appropriate escalation.
- **User experience:** Positive feedback and increased issue resolution.
- **Knowledge management:** Improved visibility into outdated documentation and information gaps.
- **Support operations:** Fewer repetitive requests and better-prepared support tickets.

Baseline measurements should be collected before the pilot so results can be compared objectively.

## 14. Future Improvements and Expansion

After evaluating the pilot, potential improvements include:

- Expanding support to additional business applications.
- Using Model Context Protocol (MCP) integrations to connect approved tools and data sources.
- Introducing AI agents for routine support tasks with defined permissions and human oversight.
- Checking application availability and reporting known service issues.
- Analyzing recurring questions to identify documentation gaps and training needs.
- Automating selected support workflows where appropriate controls are in place.
