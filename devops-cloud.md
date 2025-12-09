## 1. Intro – Why Usual Cloud Skills Aren’t Enough Anymore

* Basic cloud knowledge, Docker, Kubernetes clusters, CI/CD pipelines, and a few Terraform templates **used to be enough** to get a job around **2022–2023**.
* For **2026**, these same skills **won’t even help you get shortlisted** because almost everyone has them now.
* The **cloud industry has evolved** and the **bar is higher**:
  * Companies want engineers who understand:
    * **Automation**
    * **Intelligence**
    * **Scalability**
  * They want systems that can **scale themselves**, **fix themselves**, and **monitor themselves** as much as possible.
* If you are **still doing the same tutorials and same simple projects as everyone else**, you need to **change direction**.
* Vishaka says she will share **5 cloud skills** you need for **2026**, explaining:
  * What they are
  * Why they matter
  * How to start learning them

***

## 2. Cloud Skill #1 – GitOps and Platform Engineering

### What’s changing

* Teams are moving from traditional **DevOps** to **platform engineering**.
* Earlier: every team manually created their own **CI/CD pipeline** for each project.
* Now: companies want **internal platforms** that developers can use themselves, like a **self-service DevOps** system.

### What is GitOps?

* In **GitOps**, **everything lives in Git**:
  * Application code
  * Infrastructure
  * Configuration
  * Deployment definitions
* When you **change something in Git**, the system is **automatically updated**.
* This happens using tools like:
  * **Argo CD** – takes what you push to Git and deploys it to Kubernetes.
  * **Flux CD** – does a similar job but in a lighter, modular way.
* Result:
  * You **don’t run deployments manually**.
  * **Git becomes the single source of truth**.

### How to start (as per the video)

1. **Brush up your Git basics.**
   * She mentions a website with good hands-on Git practice (link in the video description).
2. **Learn Kubernetes fundamentals.**
   * You need basic Kubernetes knowledge to practice GitOps.
3. **Pick a project with Argo CD or Flux CD.**
   * Try to see how a **Git commit becomes a live deployment**.
   * This will give you a sense of achievement and clarity.

### Why it matters (according to the video)

* Enterprises want systems that are:
  * **Consistent**
  * **Reliable**
  * With **minimal deployment errors**
* **GitOps** helps provide exactly that.

***

## 3. Cloud Skill #2 – Infrastructure as APIs

### From “Infrastructure as Code” to “Infrastructure as APIs”

* You already may know **Terraform**, a very in-demand tool.
* But companies **don’t want huge Terraform templates** for every infrastructure need anymore.
* Instead, they want to treat **infrastructure like programmable APIs**:
  * Define a cloud resource **once**.
  * Developers **call it when needed**, just like calling an API.

### Tools mentioned

* **Crossplane**:
  * Lets you create cloud resources **through Kubernetes**.
  * Kubernetes acts as a **control plane** and **single source of truth**.
  * You write **YAML**, Crossplane reads it and provisions the cloud resources via Kubernetes.
* **Pulumi**:
  * Lets you define infrastructure using programming languages like **Python** or **TypeScript**.
  * So, **coding becomes important**.

### Why this approach is powerful

* Infrastructure becomes:
  * **Dynamic**
  * **Modular**
  * **Reusable**
  * **Versioned like code**

### How to start (from the video)

1. **Learn Terraform** and how to write configuration files.
2. **Understand how APIs work.**
3. **Get hands-on with Crossplane** in a Kubernetes cluster.
   * She suggests building a **project** with it.
4. She mentions links to **projects and tutorials** in the description.

### Why it matters for cloud teams

* Teams want **on-demand infrastructure** that:
  * **Scales across projects**
  * Works **without rewriting templates** every time.

***

## 4. Cloud Skill #3 – Observability and AIOps

### Why “monitoring” alone is not enough

* Traditional **monitoring** isn’t sufficient for modern systems.
* You now need **observability**:
  * It connects **metrics**, **logs**, and **traces**.
  * Helps you **truly understand** what’s happening inside the system.

### Tools mentioned

* **Prometheus** – for metrics.
* **Grafana** – for visualizing those metrics.
* **OpenTelemetry** – for data collection.

### What is AIOps?

* **AIOps** adds **AI** on top of observability.
* AIOps can:
  * **Detect issues**
  * **Spot patterns**
  * **Predict failures**
  * Sometimes **fix problems before humans notice them**

### How to start (from the video)

1. Revisit basics:
   * **Logs**
   * **Metrics**
   * **Alerts**
   * **Traces**
2. Get hands-on with:
   * **Prometheus**
   * **Grafana**
     (She mentions some projects in her guide.)
3. Read about **OpenTelemetry** to understand how it works.
4. Understand **how AIOps works**:
   * How it analyzes logs and anomalies.
5. If possible, **build at least one project** around AIOps.

### Why it matters

* Companies want systems that:
  * Run **continuously**
  * Have **fewer incidents**
  * Recover **faster** when things go wrong
* Incidents will still happen, but these skills reduce impact and downtime.

***

## 5. Cloud Skill #4 – AI Infrastructure and Model Deployment

### Why this is important

* **AI is everywhere**, but:
  * Getting AI models to run in **production**, at **scale**, reliably is a **separate skill**.
* That’s where **AI infrastructure engineering** comes in.

### What AI infrastructure engineers work with

* **GPUs**
* **Model inference** (serving model predictions)
* **Vector databases**
* **Model monitoring**
* **Latency optimization**
* **Scaling workloads across clusters**

### Tools mentioned

* **Triton Inference Server** – helps run AI models efficiently on GPUs.
* **Ray** – helps scale model deployments across multiple machines.
* **KServe** – a Kubernetes-native way to deploy models.

### How to start (from the video)

Assuming you already know **Docker** and **Kubernetes**:

1. Learn **how to containerize an AI model**.
2. Understand **GPU basics** and **scheduling concepts**.
3. Learn **inference fundamentals**:
   * How models are **served in production**.
4. **Deploy a model** and **track its performance**:
   * This is the **model monitoring** step.
5. She mentions that there are **good courses** linked in her guide.

### Why it matters

* Companies are **already integrating AI**.
* They need engineers who understand **both cloud and AI**.
* There is “so much AI everywhere,” so this combined skill is in high demand.

***

## 6. Cloud Skill #5 – Event-Driven Architecture and API Intelligence

### From request–response to event-driven

* Modern systems are moving away from simple **request–response** models.
* They move towards **event-driven workflows**, where:
  * Applications **react to events automatically**.
  * Events can be:
    * A **user action**
    * A **data stream**
    * An **AI output**

### Tools mentioned

* **Kafka** – moves data between services **in real time**.
* **RabbitMQ** – lets services communicate **asynchronously**.
* **Serverless options** like:
  * **AWS Lambda**
  * **Cloud Functions**
    These can run **small pieces of code whenever an event happens**.

### APIs getting smarter

* APIs now can:
  * Apply **security logic**
  * Run **model inference**
  * Make **decisions at the edge** (near the user or device).

### How to start (from the video)

1. Get familiar with **Kafka** and **RabbitMQ**.
2. If you’ve heard of **event-driven systems**, read about them more.
3. Understand **asynchronous communication**:
   * Analogy from the video:
     * Async is like **dropping a message in someone’s inbox** instead of calling them.
     * They read it when they can.
     * You **don’t need to wait on the phone**.
4. Practice by:
   * Looking for projects that involve **Cloud Functions / Lambda / other serverless options**.
   * Working a bit with **event-driven architectures**.

### Why it matters

* By **2026**, most large-scale systems will be **event-driven by default**.
* Because event-driven architectures:
  * Improve **performance**
  * Reduce **cost**
  * Increase **reliability**

***

## 7. Conclusion – How to Use These Skills for Your Career

* These **5 skills** will matter most for:
  * **Cloud engineers**
  * **DevOps engineers**
  * **AI engineers**
    in **2026**.
* If you **start practicing now**, you’ll be:
  * **Ahead of 90% of the industry**
  * More **relevant** for future roles
* You **don’t need all 5 at expert level**:
  * If you learn **2–3 of these deeply**, you’ll already be ahead of people who are still stuck on basics.
* Cloud in 2026 is **not** about:
  * Memorizing commands
* It **is** about:
  * How well you can combine **automation**, **intelligence**, and **scalability**.
* Her advice:
  * **Start small**
  * Pick **one skill**
  * Give it a **real effort**
  * By the time others are catching up, you’ll already be ahead for the new cloud roles.
* At the end, she asks viewers to:
  * Like, share, comment which skill they want to learn first
  * Subscribe for more **cloud roadmaps and guides**
