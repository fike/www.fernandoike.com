+++
title = "Licenses and how they impact a project or product"
date = 2021-02-02T09:35:09-03:00
draft = true
description = "It's a text about impacto from companies change license"
categories = ["licenças", "opensource", "portuguese"]
tags = ["licenças", "opensource", "portuguese", "elastic", "mongodb", "aws"]
+++
!["papers with law description"](/images/binding-contract-948442_640.jpg)

How to decide about what technologies, frameworks and/or platforms will be the base to develop products and services aren't many times rational decisions. They are strongest influenced by personal experience, buzzwords, etc. 

This is clear when people in the leadership role decide on A or B technology, many times the decision is too influenced by previous successful projects, a recommendation for other people, or commercial partners. There isn't any issue about how to decide like situations mentioned previously since there is a clear idea about what technology has good and bad versus how the team is prepared to adopt the tech decided.

An example is when I was CTO of EdTech, one of my responsibilities was picking technologies to develop a new platform until hire software engineers and we can decide together. The stack was [Python](https://www.python.org/) and [Django](https://www.djangoproject.com/) as backend, [PostgreSQL] as database, for frontend would one of those more popular (at least for me), [Angular](https://www.angular.io), [Reac](https://reactjs.org/) or [Vue](https://vuejs.org). We waited for frontend people to hire and discuss with them how these frameworks will use.

I chose Python and Django ([REST](https://www.django-rest-framework.org)) was Python because is a programming language with a low learning curve compared to other languages (doesn't mean it's easy), it's very popular and more smooth to hire software engineers than other languages. Another important part of the stack foundation is that any artifact will release by container, not just because containers are cool but when apply in the whole development pipeline have a gain of productivity ([DevOps State Report 2018](https://inthecloud.withgoogle.com/state-of-devops-18/dl-cd.html)). Initially using Docker and deploy VMs and nearly move to Kubernetes.  

PostgreSQL is a really cool database that we can use for kinds of purposes, most cloud providers offer it as managed service, and Python ORMs as [SQLAlchemy](https://www.sqlalchemy.org) and [Django ORM](https://docs.djangoproject.com/en/3.1/topics/db/queries/) have good support for it. In a previous AI startup that I worked on, PostgreSQL was used to store [Event Sourcing](https://microservices.io/patterns/data/event-sourcing.html) data. Thank you (Mario Idival)[https://twitter.com/marioidival] for your insight and implementation. 

Certainly, I can't say that I didn't have a bias to decide about technologies. Even though I token decisions based on good arguments, I have to recognize that I have some bias. Containers to delivery artifacts and PostgreSQL as default database were chosen base on previous projects that have success in my experience.



There isn’t any problem to make decisions but it's better when you can bring your team because will they use these technologies and become easier to identify the limits and weaknesses of each technology in your development cycle and production environment. Also, they will say they are comfortable learning that and look at other technologies without the pressure of obligation to learn base on a decision top-down.

However, there is a side that a few discuss when decide what are technologies will adopt. But, this is change after MongoDB and Elastic change license to SSPL, this becomes a subject important.

An important note: I'm not a lawyer, this analysis is an opinion. Don t use the content below as a reference, check a specialized company if want an opinion about that you adopt open source in your company.

In the startup example mentions before, most of part the snack is based on the permissive license (BSD): PostgreSQL, Django e Django REST. Python ([PSF License Agreement](https://docs.python.org/3/license.html)) and Psycopg2 ([LGPL-3](https://www.psycopg.org/license)) are “derivaded” of [GPL-2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html) and [GPL-3](https://www.gnu.org/licenses/gpl-3.0.en.html). React and [Next.js](https://nextjs.org) use [MIT](https://github.com/vercel/next.js/blob/canary/license.md) license, most of dependencies libraries of projects that we developed used [BSD](https://opensource.org/licenses/BSD-3-Clause), MIT or [Apache-2](https://opensource.org/licenses/Apache-2.0).

Many time we thought to use ElasticSearch as part of our foundation stack, but if consider today to start a project in a company while I'm writing this text I confess that I'll think two times.

#### 1. ElasticSearch isn't under an Open Source license

Always that possible I prefer to adopt technologies with open source license and have good and transparence governance. This potentializes an amazing technological and economic collaboration environment, a good example is [CNCF Landspace](https://landscape.cncf.io/) [mapped as open source](https://landscape.cncf.io/?license=open-source) that has a market cap estimate of **$10.65T**.

The [SSPL](https://www.mongodb.com/licensing/server-side-public-license) license [isn't conside Open Source](https://opensource.org/node/1099) for [Open Source Initiave](https://opensource.org/) (OSI).

#### 2. Broke the ecosystem and users become clients after the 7.11 version.

Volunteer or not, Elastic had the strongest ecosystem around Elastic that companies have growth like [Logz](https://logz.io/blog/open-source-elasticsearch-doubling-down/), [CrateDB](https://crate.io/a/cratedb-doubling-down-on-permissive-licensing-and-the-elasticsearch-lockdown/) and [Aiven](https://aiven.io/press/aiven-statement-on-license-changes-for-elasticsearch) but the ecosystem is broken because of the license change. This means that a part of a robust ecosystem (users, clients, partners, [coopetitors](https://en.wikipedia.org/wiki/Coopetition), volunteers, etc…) around an Open Source project will eliminate. It isn't Elastic that change to SSPL, [MongoDB](https://www.mongodb.com/licensing/server-side-public-license) was a pioneer, and the last year [Graylog](https://www.graylog.org/post/graylog-v4-0-licensing-sspl) change too.

Sure, it's [understandable](https://www.elastic.co/blog/why-license-change-AWS) why they change the license, but it's not something like - “[We are good and they are evil](https://www.zdnet.com/article/elastic-changes-open-source-license-to-monetize-cloud-service-use/)”.

## What's the better license?

Do you know the default consultor answer? “Depends...”

### As a technology user

Follow what developers (people and/or companies) are thinking about the future of the project that it's based on your stack. Changes like that don't arrive overnight.

### As technology user and developer too

It's the same as that phrase above but an important thing to add. If you or your organization think to contribute to a project, take a look at how the governance project happens. The projects under the Apache Foundation and CNCF have a good and clear governance process. 

### As a developer technology

The license of a project must choose base on the business model that the company wants to follow. For any kind of Open Source license that has a good case success, here some examples:

* [Canvas](https://github.com/instructure/canvas-lms) é um LMS com a licença AGPL desenvolvido pela [Instructure](https://www.instructure.com/)
* Next.js é um “React Framwork” com a licença MIT desenvolvido pela [Vercel](https://vercel.com/)
* [MariaDB](https://mariadb.org) é um banco de dados com a licença GPL-2  desenvolvido pela [MariaDB](https://mariadb.com/)
* PostgreSQL é um banco de dados com a licença BSD

There isn't any problem If you want to use in your stack some project with SSPL, but you must know that it isn't Open Source. 😉

## Referências

* [Vicky Brasseur - Elasticsearch and Kibana are now business risks](https://anonymoushash.vmbrasseur.com/2021/01/14/elasticsearch-and-kibana-are-now-business-risks)
* [Elastic - Amazon: NOT OK - why we had to change Elastic licensing](https://www.elastic.co/blog/why-license-change-AWS)
* [MongoDB - SSPL](https://www.mongodb.com/licensing/server-side-public-license)
* [Percona - Why is MongoDB’s SSPL Bad For You?](https://www.percona.com/blog/2020/06/16/why-is-mongodbs-sspl-bad-for-you/)
* [Graylog - Graylog v4.0 Licensing SSPL](https://www.graylog.org/post/graylog-v4-0-licensing-sspl)
* [OSI - The SSPL is Not an Open Source License](https://opensource.org/node/1099)
* [CNCF - Landscape - Open Source](https://landscape.cncf.io/?license=open-source)
* [Aiven statement on license changes for Elasticsearch](https://aiven.io/press/aiven-statement-on-license-changes-for-elasticsearch)
* [Zdnet - Elastic changes open-source license to monetize cloud-service use](https://www.zdnet.com/article/elastic-changes-open-source-license-to-monetize-cloud-service-use/)
* [CrateDB Doubling Down on Permissive Licensing and the Elasticsearch Lockdown](https://crate.io/a/cratedb-doubling-down-on-permissive-licensing-and-the-elasticsearch-lockdown/)
* [Logz - Truly Doubling Down on Open Source](https://logz.io/blog/open-source-elasticsearch-doubling-down/)
* [Coopetition](https://en.wikipedia.org/wiki/Coopetition)
* [Linux Foundation trainning - Open Source License for Software Developers](https://training.linuxfoundation.org/training/open-source-licensing-basics-for-software-developers/)
