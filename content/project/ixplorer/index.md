---
author: Ronny A. Hernández Mora
date: "2022-03-20"
draft: false
excerpt: ixplorer facilitates the DataOps workflow. It allows the user to review, open, and close issues for specific repositories inside RStudio.
layout: single
subtitle: An R package that integrates ixplorer (built with gitea) with RStudio
title: ixplorer
---

## [ixplorer](https://ixpantia.github.io/ixplorer/) is a package that allows users to create, close or review issues without leaving their RStudio session.

---

### What is ixplorer?

ixplorer is an R package built around gitea which is a self-hosting git service option.  The ixplorer package allows the user to review, open, and close issues for specific repositories through an interface or through functions. This involves the use of an addin within RStudio that opens an interface created with shiny, shinyWidgets, and miniUI. Also we created a logic to handle credentials with keyring for different scenarios like storing the credentials in the computer or storing the credentials for a specific amount of time (working on computers that do not belong to the user). The latest development cycle has been focused on translating the documentation of the entire package into Spanish, so it can be used by people who speak English or Spanish.



