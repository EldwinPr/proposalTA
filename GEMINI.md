# GEMINI Project Context

## Directory Overview

This directory contains a LaTeX project for a thesis proposal at the Institut Teknologi Bandung (ITB). The project is structured with a main file `ProposalTA.tex` and separate files for each chapter.

## Project Goal and Core Idea

The central theme of this thesis is to analyze the feasibility of a novel infrastructure model for deploying Enterprise Resource Planning (ERP) systems for Indonesian Micro, Small, and Medium Enterprises (UMKM).

The core idea is to propose and evaluate a **low-power device cluster** (e.g., using Single-Board Computers like Orange Pi or undervolted Mini-PCs) as a cost-effective and power-efficient alternative to mainstream solutions like cloud VPS or traditional on-premise servers. The research aims to prove that this alternative is not only cheaper but also "more than sufficient" for the typical workload of an UMKM, thus lowering the barrier to digitalization.

## Key Files

*   `ProposalTA.tex`: The main LaTeX file that brings all the other parts of the document together.
*   `daftar-pustaka.bib`: The bibliography file in BibLaTeX format.
*   `Bab I - Pendahuluan.tex`, `Bab II - Studi-Literatur.tex`, etc.: These files contain the content of each chapter.
*   `iii.1 Analisis Kondisi saat ini.txt`: A draft file for brainstorming and writing content for Chapter 3.
*   `image/`: This directory contains the images used in the document.
*   `table/`: This directory contains tables that are included in the document.

## Usage

This project is intended to be compiled using `xelatex` and `biber`. The compilation process is as follows:

1.  `xelatex ProposalTA.tex`
2.  `biber ProposalTA`
3.  `xelatex ProposalTA.tex`
4.  `xelatex ProposalTA.tex`

Alternatively, you can use a LaTeX editor with a pre-configured build chain for `xelatex` and `biber`.
