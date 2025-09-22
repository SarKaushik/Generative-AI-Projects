Smart Traffic Monitoring System Using Multi-Agent AI (Autogen)

This project demonstrates the use of Autogen's multi-agent framework to design, implement, and document a smart traffic monitoring system for an urban city. It simulates an AI-driven collaborative workflow involving multiple specialized agents, each contributing to different phases such as planning, engineering, data analysis, quality review, and report generation.

🧠 Project Overview

Urban traffic congestion and road safety remain significant challenges, especially in large metropolitan areas like Los Angeles. This project aims to address these issues by simulating a smart traffic monitoring solution using AI agents that autonomously plan, implement, analyze, and report on city infrastructure projects.

Built using Autogen and powered by GPT-4o, the system features an intelligent agent collaboration framework. Each agent is role-defined and acts according to its domain knowledge, allowing seamless interaction and task delegation.

🏗️ Agents and Their Roles

This system consists of seven specialized agents:

🧑‍💼 CityAdmin (UserProxyAgent) – The final decision-maker. No task proceeds without their approval.

🧭 CityPlanner – Breaks down the traffic monitoring project into structured steps. Assigns tasks to Engineer and DataAnalyst.

🛠️ Engineer – Implements infrastructure logic and sensors using Python and shell scripts.

📊 DataAnalyst – Interprets traffic trends and sensor data to derive meaningful insights (non-coding role).

🖥️ SystemExecutor (UserProxyAgent) – Executes code and reports any output or errors from the Engineer.

✅ Reviewer – Evaluates plans, implementation, and reports for accuracy, feasibility, and completeness.

📝 ReportWriter – Compiles a full research report covering objectives, methodology, data insights, architecture, and final recommendations.

🧰 Tech Stack

Language Model: GPT-4o (OpenAI)

Framework: Microsoft Autogen

Programming Language: Python

Execution Environment: Local execution via SystemExecutor

Key Feature: GroupChat with autonomous agent collaboration and dynamic role-based interaction

🚀 How It Works

The project kicks off when the CityAdmin agent initiates a request for a research report. This triggers a multi-step, collaborative AI workflow:

Planning: CityPlanner develops the deployment strategy.

Execution: Engineer builds the codebase, which is tested by SystemExecutor.

Analysis: DataAnalyst interprets traffic data insights.

Review: Reviewer evaluates the integrity and feasibility of the entire process.

Documentation: ReportWriter compiles a professional, human-readable report.

All communication and task handovers occur autonomously within a GroupChat of AI agents managed by a GroupChatManager.

📄 Sample Use Case

"Write a 6-paragraph research report about current issues with LA traffic in the United States and how we can implement a smart traffic monitoring system to reduce deaths by road accidents."

This query is submitted by the CityAdmin, triggering the agents to collaborate and deliver a full, technically sound report backed by simulated code, analysis, and feasibility assessments.

📌 Future Scope

Real-time data integration from traffic APIs or sensors.

Docker-based simulation and deployment.

Integration with GIS tools for geographic mapping of results.

Expand agents to include public policy advisors and legal compliance checkers.
