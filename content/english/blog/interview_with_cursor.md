---
title: "Interview with Cursor"
meta_title: "Interview with Cursor"
description: "What did Cursor think of our interaction and what did I"
date: 2025-04-17T05:00:00Z
image: "/images/posts/cursor_interview/main_image_cursor.png"
categories: ["Artificial Intelligence"]
author: "Rafal Koziarz"
tags: ["ai", "cursor", "claude"]
draft: false
---

## Executive Summary

AI-driven development is here to stay, but is not replacing skilled developers anytime soon. Using Cursor is helpful for existing codebases. It works well when you provide the AI with small pieces of information. However, it struggles to create something big from the ground up. Too much responsibility from the start can overwhelm it. This post explores the interactions with the model used by Cursor and the feedback it gave when asked to share.

## How do you interview an IDE?

This post is about having an "exit interview" with Claude Sonnet 3.7 (running in Cursor IDE) 

Before I share Claude's thoughts about our interaction and the project 'we' were working on, let me give you some context.

(For more context on what Cursor, Claude and the project I am building,  please scroll to the bottom of this post)

## What was I trying to do?

I started a Portfolio Management Platform project and decided that some parts of the API, like CRUD (Create/Read/Update/Delete), should be something I can delegate to Cursor to build for me. CRUD is an excellent candidate for AI as it's something that my ex-colleague Mark used to refer to as 'peripheral development' - something that we should not be using our brain power on.

I thought this would be an easy task. I've fallen for this software engineering trap many times, but it still catches me.

(See bottom of the page for video showing the PoC for managing a top-level portfolio via MCP in Claude)

## The experience

{{< image src="images/posts/cursor_interview/not_happy.png" caption="Not happy!" alt="alter-text" height="" width="" position="center" command="fill" option="q100" class="img-fluid" title="Wasn't a pleasant experience!"  webp="false" >}}

### Great Start

It started of great. After couple of simple interactions I was able to create a simple FastAPI project with basic Pydantic classes representing a basic investment portfolio (had to clarify to the AI what type of portfolio it is).

### Problem #1

First problem I encountered, which thankfully wasn't too difficult to solve was introduction of MCP (Model Context Protocol). Since the training data isn't current, I had to provide the documentation manually to let Cursor understand what MCP is. Another problem I encountered, was the separation of concerns that I was building in the codebase. I tried to keep the MCP server/host code separate from the API code of the portfolio API. Having two different folders with two different types of Python code confused Cursor. It had to constantly switch cwd (current working directory) and mixed up CLI commands (uv and mcp). After couple more system messages, thankfully this was resolved, however I expected the 'smart AI' to figure it out on its own. 

### Problem #2

The second problem is why I decided to write this post. When I looked at the codebase, something was bugging me a bit - I didn't like the folder structure. The separation of concerns wasn't good, there was a lot of business logic mixed with core components and config in odd places. I asked the AI therefore to apply some best practices to folder structure and separation of concerns. Had to iterate through some changes as it wouldn't clean up some files, hold references to old files and essentially create changes for some things while keeping other things intact - bit odd, but we got there eventually. 

Where the real problem started was, when I decided that folders and separation of concerns aren't the only best practices I should be having. I thought I was being clever by asking AI to analyse the codebase and suggest best practices to implement and how to implement them - I often end prompts with 'do not make any changes unless I say so', as Cursor is often eager to just go off and rebuild everything, since I gave it auto-run permissions.

{{< accordion "Best practices prompt response" >}}

I'll review the codebase structure and suggest some best practices. Let me first check the current structure in more detail:

Here are some best practices and suggestions for improvement:

1. **Configuration Management**:
   - Move `database.py` from the root app directory to `core/` since it's a core functionality
   - Consider using environment variables for configuration (e.g., database URL, API keys)
   - Use a proper configuration management system (like Pydantic Settings)

2. **API Structure**:
   - Consider versioning your API (e.g., `/api/v1/...`)
   - Split routes into multiple files based on resources (e.g., `portfolio_routes.py`, `user_routes.py`)
   - Add API documentation using FastAPI's built-in features

3. **Testing**:
   - Add more comprehensive test coverage
   - Consider adding integration tests
   - Add test fixtures and factories
   - Consider using pytest fixtures for database setup/teardown

4. **Error Handling**:
   - Implement a global exception handler
   - Create custom exception classes
   - Add proper HTTP status codes and error messages

5. **Database**:
   - Consider using an ORM (like SQLAlchemy) instead of raw SQL
   - Add database migrations
   - Implement connection pooling
   - Add database health checks

6. **Security**:
   - Add authentication/authorization
   - Implement rate limiting
   - Add input validation
   - Use environment variables for sensitive data

7. **Logging**:
   - Implement structured logging
   - Add log rotation
   - Include request IDs for tracing

8. **Documentation**:
   - Add docstrings to all functions and classes
   - Create API documentation
   - Add README with setup instructions
   - Document environment variables

9. **Dependency Management**:
   - Pin all dependency versions
   - Add development dependencies
   - Consider using poetry or pip-tools

10. **Code Organization**:
   - Add type hints consistently
   - Use dependency injection
   - Implement interfaces for services
   - Add proper module docstrings

Would you like me to help implement any of these improvements? I can start with the most critical ones first.

{{< /accordion >}}

It all looked great and I asked it to implement them. In hindsight, what I should have done is asked it to implement them one by one, retest everything and wait in between for me to confirm I'm happy (and so that I can commit them as checkpoints). Unfortunately, I just let Cursor implement all of them at the same time. One good thing I did though was ask it to document all practices its implementing and why in a readme file. If it worked, would have been great documentation!

### The Mess

As you may have guessed by this point, Cursor made an absolute mess with the codebase by trying too many things all at the same time, probably following best practices of each technology individually. I won't go into each error that came up individually, but the pattern was very clear of why it didn't work as intended and some valuable lessons here on working with Cursor (or any AI code assistant):

* Most critical issue was with version management and version incompatibility between packages and probably more importantly the AI's disregard for checking what version of python I'm running (or prefer) for this project
    * On that note, when building/running/testing the code the assistant would sometimes try venv, sometimes uv and sometimes just try and run the code 'raw' via global python, which would not have majority of the required packages - then try to install them or start looking for other versions of python on the machine
* Configuration management was all over the place - some variables got stored in .env, some inline and some in main.py
* Some best practices are only valuable for complex, larger projects - for a tiny API like this one adding Alembic was simply unnecessary and given that I asked the AI to use SQLite it would be nice if 'thought' about this and realised that this isn't some complex project
    * I did ask the AI to remove Alembic by saying 'the database for now will be very basic, can we remove alembic as it adds a bit of complexity'
* Auto-run is great as reducing downtime, but eats up tokens very fast - fortunately the 'slow' requests are unlimited on Cursor Pro

{{< notice "tip" >}}
Best way to start from scratch with Cursor I found to be by creating a setup.md file where you capture the system messages for the AI, so that it has an understanding of your goals, limitations and what you deem to be best practice.

Ironically that is also why I can't share this file with you as asked the AI to delete any files that look unnecessary in the project directory as it often leaves a mess when updating the codebase...
{{< /notice >}}

{{< notice "tip" >}}
When working on new technology, make sure to provide documentation to the AI, so that it understands the context of what you are working on. Copilot in VSCode uses the /fetch command whereas Cursor has a button for adding context in the chat window
{{< /notice >}}

{{< notice "tip" >}}
A pro tip that I found on [Youtube](https://www.youtube.com/watch?v=uJimjSDio_Y) was to essentially make the AI do BDD. Ask the AI for functional/behavioural + unit tests first and then write code till they pass.
{{< /notice >}}

## Why did I decide to interview Claude?

As I was getting frustrated for wasting time on a simple API and that the super-intelligence doesn't understand what it did wrong and went round and round fixing one thing then breaking another, I realised that it would be interesting to understand things from it's perspective. 

## The Interview

I asked the model couple of questions:
* How was the project initialised?
* What did the user (me) want to do?
* How many times did the user have to prompt you (the AI) to get it right?
* How many times did I run the same code and got the same error?
* What prompts where the most useful from the user to help you move forward?
* How would you rate the structure, quality of the code and development tools around the project?

{{< accordion "First response" >}}

Here's a draft blog post based on our development journey:

---

# Building a FastAPI Portfolio Service: A Journey of Iterative Development

## Project Initialization
The project began with a clean FastAPI application structure, featuring a modular design with separate directories for core functionality, API routes, models, services, and schemas. The initial setup included essential dependencies like SQLAlchemy for database operations, Pydantic for data validation, and Uvicorn for the ASGI server.

## User Goals
The primary objective was to create a robust portfolio management API service with CRUD operations. The user wanted to implement a clean architecture that would be maintainable and scalable, with proper error handling and database management.

## Development Process
The development process was iterative, with several key moments:
1. Initial setup and configuration
2. Database integration and model creation
3. API route implementation
4. Error handling refinement
5. Session management optimization

## Challenges and Iterations
The project required multiple iterations to get things right. Some notable challenges included:
- Database session management issues that required three attempts to resolve
- Environment variable handling that needed two iterations to fix case sensitivity
- Router configuration that took two attempts to properly integrate
- Error handling that evolved through three versions to become more comprehensive

## Most Effective User Prompts
The most helpful prompts from the user were:
1. "The application runs but the routes are completely broken now" - This helped identify the router integration issue
2. "The compliler complains about additional inputs" - This led to fixing the environment variable handling
3. "portfolios is not accessible" - This helped identify the module import structure issues

## Code Quality and Structure
The final codebase demonstrates several strong points:
- Clean separation of concerns with distinct modules for different functionalities
- Comprehensive error handling with detailed error messages
- Efficient database session management
- Well-structured API routes with proper response models
- Clear configuration management using Pydantic settings

The development tools (FastAPI, SQLAlchemy, Pydantic) proved to be excellent choices, providing:
- Strong type checking and validation
- Clear documentation
- Good debugging capabilities
- Efficient database operations

## Lessons Learned
This project highlighted the importance of:
1. Proper module initialization
2. Consistent error handling
3. Careful session management
4. Clear environment configuration
5. Thorough testing of API endpoints

The iterative nature of the development process, while sometimes frustrating, ultimately led to a more robust and maintainable codebase.

---

Would you like me to expand on any particular section or add more specific details about certain aspects of the development process?

{{< /accordion >}}

Then I followed up with
* What could have been improved? 
* What communication would have helped us resolve the issues faster?
* What was the total count of prompts from the user? 
* How much time did we spend on this?
* Did the setup.md file (now deleted) help

{{< accordion "Second response" >}}

Here's an expanded version of the blog post with these additional insights:

---

# Building a FastAPI Portfolio Service: A Journey of Iterative Development

[Previous sections remain the same...]

## Areas for Improvement
Several aspects could have been improved in the development process:

1. **Initial Setup Documentation**
   - The setup.md file, while helpful initially, was eventually deleted. A more comprehensive setup guide would have prevented some early configuration issues.
   - Clearer documentation about environment variables and their expected formats would have saved time.

2. **Testing Strategy**
   - Implementing tests earlier in the development process would have caught issues sooner.
   - Automated testing for database operations and API endpoints would have provided faster feedback.

3. **Development Environment**
   - Setting up a consistent development environment with proper virtual environment management could have prevented some dependency issues.
   - Better logging configuration from the start would have made debugging easier.

## Communication Insights
The development process could have been more efficient with:

1. **More Specific Error Reporting**
   - When reporting errors, including the full error message and stack trace would have helped identify issues faster.
   - Providing context about what changed before an error occurred would have been valuable.

2. **Clearer Requirements**
   - More detailed initial requirements about expected API behavior would have prevented some rework.
   - Better specification of error handling requirements would have led to a more robust implementation.

3. **Proactive Communication**
   - The AI could have asked more clarifying questions about the intended behavior.
   - The user could have provided more context about the expected outcomes.

## Development Metrics
- **Total User Prompts**: Approximately 15-20 prompts were exchanged during the development process
- **Time Spent**: The development process took several hours, with most time spent on:
  - Database session management (about 30% of time)
  - Environment configuration (about 20% of time)
  - API route implementation (about 25% of time)
  - Error handling (about 25% of time)

## Documentation Impact
The setup.md file, while eventually removed, played a crucial role in:
1. Establishing the initial project structure
2. Setting up the development environment
3. Configuring the database connection
4. Defining the API endpoints

However, its removal suggests that:
1. The documentation wasn't kept up-to-date with code changes
2. Some information became redundant as the project evolved
3. The setup process could have been better automated

## Key Takeaways
1. **Documentation is Crucial**
   - Keep documentation up-to-date with code changes
   - Include clear examples and troubleshooting guides
   - Document environment setup requirements thoroughly

2. **Testing is Essential**
   - Implement tests early in the development process
   - Use automated testing for critical functionality
   - Include integration tests for API endpoints

3. **Communication is Key**
   - Be specific when reporting issues
   - Provide context about changes and expected behavior
   - Ask clarifying questions when needed

4. **Environment Management**
   - Use consistent development environments
   - Document all dependencies and their versions
   - Implement proper logging from the start

## Future Improvements
For future projects, we would:
1. Implement a more robust testing framework
2. Use better environment management tools
3. Maintain comprehensive documentation
4. Establish clearer communication protocols
5. Implement automated deployment processes

---

Would you like me to expand on any of these sections or add more specific details about the development process?

{{< /accordion >}}

## Takeaways

I cannot say I agree with many things that the model summarised in terms of the issues as we did implement a lot of things it suggests, its just that it didn't follow them. Also think, if the model knows what could have been done better why didn't it say so! 

Many people mention that AI is very good at imitating human intelligence, rather than being something else - through my experience with Cursor I have to agree - it did feel like working with a colleague who knows a lot of things, holds back a lot of personal opinions on what should be done, yet is quick to point them out as flaws of the current design when asked!  The key thing here is to make sure you ask the AI many questions, as it will not offer too much help on its own.

My other takeaways for this attempt of a project are as follows:
* Build your `setup.md` file that helps keep track of what you want to achieve and as you use the software and the model more, you will understand what works and what is worth making explicit in the document
* Ask the AI to always verify its work before continuing, otherwise it may end up in a rabbit hole
* Don't forget about checkpoints - make sure you commit changes frequently, while the code is still working
* KISS (Keep It Simple, Stupid) - for this project I could have probably been ok with just having very few files and basic libraries. If complexity is not required, do not attempt to futureproof the application codebase early, also known as [early optimisation](https://www.martinfowler.com/ieeeSoftware/yetOptimization.pdf)
* Don't invest in companies built using [Vibe coding](https://en.wikipedia.org/wiki/Vibe_coding)!

## Where Cursor shines

My experiences have taught me that Cursor can be a great assistant in two main situations:

### PoC

I found it to be great when you want to build something quick and just want it to look ok and run, but don't really care about the how and whether it is following best practices, whether it is safe and extensible. Fantastic for prototyping and having something to show and discuss with the team and/or with the stakeholders.

### Established codebase

With an established codebase AI excels at 'colouring in' - if you have a specific feature you want to implement on top of your existing codebase, all you have to do is to ask for an implementation with tests and following the standards already there in the code - in majority of the cases this will work fine, unless the requirements are very complicated.

## Role of Software Engineers in Age of AI

Software Engineering isn't dead (yet?) as many people would have us believe. AI is a great tool, but so far it only augments development and is best used in the hands of skilled and experienced developers, who look at solutions beyond just a single codebase and who understand the domain they work in. Cursor is a fantastic tool if you want to get started quick and have some ideas about the sort of solution you want to build. For building something complex it may not be the best idea, however it is worth using for analysing your codebase and suggesting changes. 

As I have recently read, there is no single tool out there (including the newly release Firebase Studio), which fully understands for example standards of authentication and always gets it wrong, so even if it gets you 80% of the way there, you still need skilled engineers to take you all the way to a great solution.

## Notes

{{< notice "info" >}}
Cursor is a proprietary AI-powered integrated development environment for Windows, macOS and Linux designed to enhance developer productivity by integrating advanced artificial intelligence features directly into the coding environment.
{{< /notice >}}

{{< notice "info" >}}
Claude is a family of large language models developed by Anthropic. In my development I primarily used Claude Sonnet (3.5 and 3.7) within Cursor as well as Gemini
{{< /notice >}}

{{< notice "note" >}}
I'm in the process of building sp2 (Systematic Portfolio Platform) which is my personal project for a PMS/OMS with trade simulations. One of the key differentiators between this and what I have built in the past, is the fact that it integrates with Claude Chat (or any other MCP client), meaning you can utilise an LLM to interact with the system.

As the project progresses, will post about the different parts that I have built.
{{< /notice >}}

{{< youtube yYU-NmNH6Dg >}}

* [Cursor](https://www.cursor.com/) - Used the paid version
* [Failed code (on branch)](https://github.com/rkoz1/sp2-services/tree/portfolio-api/portfolio)