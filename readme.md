# MDS in a Box, using an all-FOSS stack

## Introduction

Thanks to [Benn Stancil's amazing Substack](https://benn.substack.com/p/is-excel-immortal), I came across [this article](https://duckdb.org/2022/10/12/modern-data-stack-in-a-box.html) on DuckDB's website, explaining how to create a "Modern Data Stack in a box," using DuckDB, Meltano, dbt, and Apache Superset. It's written to use the Windows Subsystem for Linux, but I have this hideously low-powered laptop sitting around for testing out lightweight setups, so I'm going to try this on Linux Mint.

Here, the pieces of the "Modern Data Stack" are going to include the following:

- A tool to extract data from source files
- A data warehouse in which to store that data
- A tool to transform and analyze the data in the warehouse
- A tool to create data visualizations and reports

So that's our goal; get all of these tools running on my crummy laptop, analyze some data, and maybe tell a story while we're at it. The tech is the goal here, but we *do* need to decide our context; what dataset do we want to analyze?

## The Dataset

The World Bank Group maintains a [dataset](https://genderdata.worldbank.org/en/topics/violence) on gender-based violence (GBV). It includes over 200 attributes ranging from beliefs about GBV, to prevalence of GBV, to contextual indicators relating to GBV, such as GDP and government spending on education. It's a global dataset with a truly impressive reach (265 countries are represented), but as American culture is the only culture I feel qualified to comment on, I'll only be looking at US data for this project.

## The "In a Box" Part

We often say "Out of the Box" meaning "Ready to Go," e.g. "The new robot vacuum I bought just worked out of the box," or "The software required very little configuration; out of the box, it was ready to ingest and analyze our data." Part of this project is going to be putting things *into* the box as well as we can so that the MDS we are building can be readily used with as little configuration as possible. A lot of weight here is going to be pulled by creating a **Makefile** where we can declaratively handle the configuration. This Makefile will then be built using the [GNU Make tool](https://www.gnu.org/software/make/).