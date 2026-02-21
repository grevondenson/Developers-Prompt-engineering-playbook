[10-introduction-14-debbuging-example-poor-vs-improved-12-foundations-of-effective-code-promptin.md](https://github.com/user-attachments/files/25457554/10-introduction-14-debbuging-example-poor-vs-improved-12-foundations-of-effective-code-promptin.md)
# 1.0 Introduction

AI-powered coding assistants are now integral to developer workflows. They can autocomplete functions, suggest bug fixes, and even generate full modules or MVPs. The quality of output from these tools relies on the precision and clarity of the prompt you give. As such, **prompt engineering** has become a vital skill. This guide explores practical ways to systematically craft effective prompts for common software development scenarios.

---

# 1.1 Before Prompting

AI pair programmers are powerful allies, but they have no prior knowledge about your project or intent beyond what you supply. The richer and more precise the context, the better the AI’s output.

### Key Prompt Techniques

- **Role Prompting**  
  - “You are a senior {language} developer. Review this function for {goal}.”  
    *Purpose: Simulate expert-level code review, debugging, or refactoring.*

- **Explicit Context Setup**  
  - “Here's the problem: {summary}. The code is below. It should do {expected behaviour}, but instead it's doing {actual behaviour}. Why?”  
    *Purpose: Frame the problem to avoid generic responses.*

- **Input/Output Examples**  
  - “This function should return {expected output} when given {input}. Can you write or fix the code?”  
    *Purpose: Show intent through examples.*

- **Iterative Chaining**  
  - “First, generate a skeleton. Next, add state. Then handle API calls.”  
    *Purpose: Break large tasks into steps.*

- **Debug with Simulation**  
  - “Walk through the function line by line. What are the variable values? Where might it break?”  
    *Purpose: Simulate runtime behavior to expose hidden bugs.*

- **Feature Blueprinting**  
  - “I'm building {Feature}. Requirements: {bullets} using: {tech stack}. Please scaffold the initial component and explain your choices.”  
    *Purpose: Kick off feature development with AI-led planning.*

- **Code Refactor Guidance**  
  - “Refactor this code to improve {goal}, such as readability, performance, idiomatic style. Use comments to explain.”  
    *Purpose: Align refactors with your goals.*

- **Ask for Alternatives**  
  - “Can you rewrite this in a functional style? What about a recursive version?”  
    *Purpose: Explore multiple implementation strategies.*

- **Rubber Ducking**  
  - “Here's what I think this function does: {your explanation}. Am I missing anything? Any bugs?”  
    *Purpose: Let the AI challenge your understanding.*

- **Constraint Anchoring**  
  - “Please avoid recursion. Stick to ES6 syntax. Optimize for memory. Here's the function.”  
    *Purpose: Prevent incompatible or overreaching patterns.*

---

# 1.2 Foundations of Effective Code Prompting

Prompting an AI coding tool is like communicating with a literal collaborator. You need to guide the AI clearly for useful results.

### Core Principles

- **Provide Rich Context**
  - Specify programming language, frameworks, libraries, relevant code, errors, and expected outcomes.
  - Example:  
    > "I have a Node.js function using Express and Mongoose that should fetch a user by ID, but it throws a TypeError. Here's the code and error."

- **Be Specific About Your Goal**
  - Vague queries give vague answers.
  - Example:  
    > "This JavaScript function returns undefined. Given the code below, can you help identify why and how to fix it?"

- **Break Down Complex Tasks**
  - Divide multi-step problems into smaller, manageable parts.
  - Example:  
    > "First, generate a React component skeleton. Next, add state management. Then, integrate the API call."

- **Include Examples of Inputs/Outputs**
  - Provides clarity and reduces ambiguity.
  - Example:  
    > "Given [3,1,4], this function should return [1,3,4]."

- **Leverage Roles or Persona**
  - Prime the assistant for style and depth.
  - Example:  
    > "Act as a senior React developer and review my code for bugs."

- **Iterate and Refine**
  - Prompt engineering is iterative. Review, follow up, and coach the AI.
  - Example:  
    > "That solution uses recursion, but I'd prefer an iterative approach—can you try again?"

- **Maintain Code Clarity and Consistency**
  - Well-structured code and comments help AI continue your patterns.

---

# 1.3 Prompt Patterns for Debugging Code

Debugging with AI is effective if you present the problem clearly.

### Effective Debugging Prompts

- **Describe the Problem and Symptoms**
  - Include what’s wrong, what should happen, code snippet, and error message.
  - Example:  
    > "I have a JavaScript function that should sum an array, but it returns NaN. Here’s the code..."

- **Step-by-Step or Line-by-Line**
  - Ask the AI to walk through code execution.
  - Example:  
    > "Walk through this function line by line and track the value of total."

- **Minimal Reproducible Examples**
  - Provide small, focused code snippets that reproduce the bug.
  - Example:  
    > "Here's a pared-down example that triggers the error..."

- **Ask Focused Questions and Follow-ups**
  - Directly ask for fixes or explanations.
  - Example:  
    > "What causes the issue, and how can I fix it?"  
    > "Can you explain why that change works?"

---

# 1.4 Debugging Example: Poor vs. Improved Prompt

This section demonstrates the impact of prompt quality when debugging a Node.js function that maps users by ID.

### Buggy Function Example

```js
// Buggy function: converts array of users to a map by ID
function mapUsersById(users) {
  const userMap = {};
  for (let i = 0; i <= users.length; i++) { // Incorrect: <= will go out of bounds
    const user = users[i];
    userMap[user.id] = user;
  }
  return userMap;
}

// Example usage:
const result = mapUsersById([{ id: 1, name: "Alice" }]);
```

**Issue:**  
The function uses `i <= users.length`, causing an out-of-bounds error and `user` becomes `undefined` on the last iteration.

### Poor Prompt Example

> "why isn't my mapUsersById function working?"

**AI Response:**  
Generic guesses about possible issues (e.g., wrong input type, user object structure, etc.), not directly addressing the bug.

### Improved Prompt Example

> “I have a JavaScript function mapUsersById that should convert an array of user objects into a map (object) keyed by user ID. However, it throws an error when I run it. For example, when I pass `[{id: 1, name: "Alice"}]`, I get `TypeError: Cannot read property 'id' of undefined`. Here is the function code: ... It should return `{ "1": {id: 1, name: "Alice"} }`. What is the bug and how can I fix it?”

**AI Response:**  
Pinpoints the loop boundary error (`i <= users.length`), explains why it occurs, and provides the fix:

```js
for (let i = 0; i < users.length; i++) {
  const user = users[i];
  userMap[user.id] = user;
}
```

**Summary:**  
Detailed prompts with scenario, code, and symptoms enable precise, actionable AI responses.

---

# 1.5 Prompt Patterns for Refactoring & Optimization

AI assistants excel at refactoring code, but only if you clarify your goals.

### Refactoring Prompt Strategies

- **State Refactoring Goals Explicitly**
  - Example:  
    > "Refactor this function to improve readability and maintainability (reduce repetition, use clearer variable names)."  
    > "Optimize this algorithm for speed—it's slow on large inputs."

- **Provide Code Context**
  - Include the relevant function, class, or section, plus environment details if needed.

- **Encourage Explanations**
  - Request explanations to learn from the refactor and verify correctness.
  - Example:  
    > "Please suggest a refactored version and explain the improvements."

- **Use Role Play**
  - Example:  
    > "Act as a seasoned TypeScript expert and refactor the code to align with best practices."

### Refactoring Example: Poor vs. Improved Prompt

#### Original Code

```js
// Original function: Fetches two lists and processes them
async function getCombinedData(apiClient) {
  // Fetch list of users
  const usersResponse = await apiClient.fetch('/users');
  if (!usersResponse.ok) { throw new Error('Failed to fetch users'); }
  const users = await usersResponse.json();

  // Fetch list of orders
  const ordersResponse = await apiClient.fetch('/orders');
  if (!ordersResponse.ok) { throw new Error('Failed to fetch orders'); }
  const orders = await ordersResponse.json();

  // Combine data
  const result = [];
  for (let user of users) {
    const userOrders = orders.filter(o => o.userId === user.id);
    result.push({ user, orders: userOrders });
  }
  return result;
}
```

#### Underspecified Prompt

> "Refactor the above getCombinedData function"

**AI Response:**  
Refactors code, combines fetches in parallel, but assumes error handling and performance preferences.

#### Goal-Oriented Prompt

> "Refactor to eliminate duplicate code and improve performance. Avoid repeating fetch logic; fetch lists in parallel if possible; keep error handling for each fetch; improve data combination using efficient lookup; provide code with comments."

**AI Response:**  
Addresses each goal, provides clean, efficient code with separate error handling and improved data combination.

### Additional Tips

- Refactor in steps
- Ask for alternatives
- Combine refactoring with explanation
- Validate and test the refactored code

---

# 1.6 Modern Debugging Scenarios

Modern front-end and full-stack apps introduce new debugging patterns, especially with frameworks like React and Next.js.

### Example: React Hook Dependency Bug

**Poor Prompt:**  
> "My useEffect isn't working right"

**Enhanced Prompt:**  
> "I have a React component fetching user data, but it's causing infinite re-renders. Here's my code:  
> `const UserProfile = ({ userId }) => { ... useEffect(() => { fetchUser(userId).then(setUser).finally(() => setLoading(false)); }, [userId, setUser, setLoading]); ... }`"

### Example: State Architecture for Next.js

**Poor Prompt:**  
> "Build the state management for my Next.js ecommerce app"

**Enhanced Prompt:**  
> "I'm building a Next.js 14 e-commerce app and need state management.  
> Requirements: product listing, shopping cart, user auth, notifications, strict TypeScript, server-side data fetching, persistence across navigation.  
> Should I use multiple Zustand stores, React Query, or a single store? Please provide a recommended architecture with code examples."

---

# 1.7 Prompt Patterns for New Features

AI code assistants can help build new features or integrate them into existing codebases.

### Strategies

- **Start with High-Level Instructions and Drill Down**
  - Example:  
    > "Outline a plan to add a search feature that filters products by name in a React app with products fetched from an API."

- **Provide Relevant Context or Reference Code**
  - Example:  
    > "Here is an existing UserList component. Now create a ProductList component with a search bar."

- **Mention Coding Style or Architecture**
  - Example:  
    > "We use Redux for state management—integrate search state into the Redux store."

- **Use Comments and TODOs as Inline Prompts**
  - Example:  
    > `//TODO: Validate the request payload (ensure name and email are provided)`

- **Provide Input/Output or Usage Examples**
  - Example:  
    > "Implement formatPrice(amount) so that 2.5 returns '$2.50'."

- **Iterate and Clarify**
  - If the first draft isn’t right, specify constraints or preferences for the next iteration.

---

# 1.8 Common Prompt Anti-Patterns & How to Avoid Them

Certain mistakes repeatedly lead to poor AI responses. Below are common anti-patterns and their remedies:

| Anti-pattern                       | Problem                                                      | Solution                                         |
|-------------------------------------|--------------------------------------------------------------|--------------------------------------------------|
| The vague prompt                    | Lacks detail; gets generic or irrelevant code                | Add context and specifics                        |
| The overload prompt                 | Asks for too many things at once                             | Split into focused tasks                         |
| Missing the question                | No clear ask; AI doesn't know what to do                     | Always include a clear question or goal          |
| Vague success criteria              | "Make this faster"—unclear metric or constraint              | State explicit goals and constraints             |
| Ignoring AI clarifications          | Miss opportunities to clarify or correct                     | Treat as a conversation; answer follow-up Qs     |
| Varying style or inconsistency      | Confuses the model; mixes formats                            | Keep style consistent, specify preferred styles  |
| Vague reference like "above code"   | AI may lose track in a long thread                           | Quote code again, or name the function/class     |

### Rewriting Prompts

- Identify what's missing or wrong in the AI's response.
- Emphasize requirements in a revised prompt.
- Break down requests further if necessary.
- Start fresh if the thread gets stuck.

---

# 1.9 Conclusion

Prompt engineering is a practical and evolving discipline, essential for developers leveraging AI code assistants. Through systematic approaches—providing context, explicit goals, sample inputs/outputs, iterating, and using roles—you can transform the AI into a valuable coding partner.

- **Debugging:** Provide detailed context to help the AI find and fix bugs efficiently.
- **Refactoring:** State your goals clearly and ask for explanations to learn and verify.
- **Feature Implementation:** Guide the AI step by step, referencing code and style.
- **Avoiding Anti-Patterns:** Ensure prompts are specific, focused, and conversational.

Approach AI as a junior teammate you’re coaching. With clarity, patience, and thoroughness, you amplify your productivity and learn new patterns along the way.

```card
{
    "title": "Prompt Engineering Takeaway",
    "content": "Treat prompt engineering as a conversation. The more context and clarity you provide, the more the AI can help you debug, refactor, and build features effectively."
}
```
