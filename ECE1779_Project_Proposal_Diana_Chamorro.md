# **ECE1779 – Introduction to Cloud Computing (Fall 2025)**  
## **Project Proposal**  

**Title:** Cloud-Native Network Health Dashboard  
**Student:** Diana Chamorro Zuleta  
**Deployment Provider:** DigitalOcean  
**Orchestration:** Kubernetes (DOKS)  
**Database:** PostgreSQL with Persistent Volume  
**Advanced Features:** Authentication (JWT) and CI/CD Pipeline (optional Backup & Recovery)

---

## **1. Motivation**

### **Problem Statement**  
I currently work full-time as a Network Engineer at Rogers Communications, where I’ve spent the past four years working on large-scale network design, deployment, and performance optimization projects. Through this experience, I’ve seen how major telecom operators monitor and maintain network reliability using enterprise-grade tools and complex infrastructure. However, I’ve also noticed a consistent gap in the industry: smaller organizations and startups often lack access to affordable, user-friendly tools for monitoring their own network performance.

While large corporations rely on platforms like Datadog or Cisco ThousandEyes to track latency, uptime, and packet loss, these tools are expensive and require significant setup and licensing costs. Smaller teams, local businesses, and even independent developers rarely have the resources or technical staff to implement such systems. Yet, reliable connectivity is just as important for them as it is for large companies; a few minutes of downtime can affect operations, reputation, or online sales.

That’s where my project idea comes from. I want to build a lightweight, cloud-based Network Health Dashboard that gives smaller users some of the same visibility that big enterprises have, but in a simpler, more accessible way. The goal is to create a web application that continuously checks the health of network endpoints (such as websites, APIs, or servers) and provides clear, visual insights into their performance. Users will be able to log in, register the endpoints they care about, and view metrics such as response time, uptime percentage, and latency trends through a clean, intuitive dashboard.

The system will run entirely in the cloud using modern tools like Docker and Kubernetes, meaning it can stay online 24/7 without depending on any local computer. Data will be stored safely in a PostgreSQL database, and monitoring results will persist across restarts.  

This project combines my professional background with the technical skills developed in this course. It’s designed to demonstrate my understanding of containerization, orchestration, state management, and monitoring — but more importantly, it aims to fill a real-world need by providing a practical, affordable solution that smaller organizations can use to monitor their services without needing an enterprise budget or a full IT department.

---

### **Target Users**  
This project is aimed at people who need a simple, affordable way to track how their websites or online services are performing. It’s especially useful for developers and DevOps students who want to monitor the uptime and response time of their APIs or small applications.

It can also benefit network engineering students who want a hands-on way to explore cloud-based monitoring and data visualization. Lastly, it’s practical for independent creators or small companies who host projects on platforms like DigitalOcean and want clear, transparent insights into how their sites are doing — without paying for expensive tools.

---

### **Existing Solutions and Limitations**  
Popular tools like Datadog, Pingdom, and UptimeRobot already offer network monitoring, but they are often costly, closed-source, and overly complex for small-scale use. This project takes a simpler and open approach, using containerized cloud technologies to give users transparency, control, and flexibility — all while keeping costs low and setup easy.

---

## **2. Objective and Key Features**

### **Objective**  
The goal of this project is to build and deploy a cloud-based web application that tracks the performance of network endpoints such as websites and servers. It will measure and display metrics like response time and uptime, store results in a database, and send alerts when performance drops below a set threshold.

The system will be fully containerized using Docker and managed with Kubernetes on DigitalOcean, ensuring reliability and scalability. It will also include built-in monitoring and automation pipelines, showing how modern cloud technologies work together in an end-to-end deployment.

---

### **Core Features**  

- **Containerization & Local Development:**  
  The entire application — including the backend, worker, frontend, and database — will run inside Docker containers. For local development, Docker Compose will manage all components together, making it easy to test and debug before deployment.

- **Database & State Management:**  
  All user information, endpoint data, and measurement results will be stored in a PostgreSQL database. Persistent volumes will ensure data durability even after restarts or updates.

- **Backend API:**  
  The backend will be built with FastAPI, handling user authentication (JWT), CRUD operations for endpoints, and REST APIs for retrieving metrics.

- **Worker / Scheduler:**  
  A background Python job (Kubernetes CronJob) will regularly check each registered endpoint and store new data in the database.

- **Frontend Dashboard:**  
  A React (Vite) web interface will display endpoint performance through charts and summaries, helping users easily track uptime and latency trends.

- **Deployment & Orchestration:**  
  The system will be deployed on DigitalOcean Kubernetes (DOKS) using Deployments, Services, PersistentVolumeClaims, and an HTTPS Ingress for secure access.

- **Monitoring & Observability:**  
  CPU, memory, and disk usage will be tracked using DigitalOcean’s built-in tools. Prometheus and Grafana dashboards will provide additional visibility into latency and API performance.

- **Advanced Feature #1 – Authentication & Security:**  
  JWT authentication, password hashing, and HTTPS will ensure secure user access.

- **Advanced Feature #2 – CI/CD Pipeline:**  
  GitHub Actions will automate the build and deployment process, pushing Docker images to the DigitalOcean Container Registry and applying updates to Kubernetes.

- **Optional Feature – Backup & Recovery:**  
  Automated PostgreSQL backups to DigitalOcean Spaces for data recovery.

---

### **Database Schema (Initial Draft)**  

To manage data efficiently, the application will use a PostgreSQL relational structure focused on reliability and scalability. Each table serves a clear purpose and links to others logically:

- **Users** – Stores account information, including email, password hash, and creation date.  
- **Endpoints** – Lists the websites or servers each user monitors, linked to their user ID.  
- **Measurements** – Records each monitoring event, saving latency, status (“up/down”), and timestamp.  
- **Alerts** – Logs alerts triggered by performance issues, including messages and resolution status.

This schema forms the foundation for user accounts, endpoint management, and performance history while remaining flexible for future enhancements such as team monitoring or notifications.

---

### **How These Features Fulfill the Course Project Requirements**  
This project meets all technical requirements in the ECE1779 course handout. It uses Docker and Docker Compose for containerization, PostgreSQL for state management, and DigitalOcean Kubernetes (DOKS) for orchestration and deployment. Monitoring and observability are implemented using both DigitalOcean metrics and Prometheus/Grafana dashboards.  

At least two advanced features are included: JWT authentication for security and a CI/CD pipeline for automation. Together, these components demonstrate a complete understanding of cloud-native development — from building and deploying to monitoring and maintaining a stateful web application.

---

### **Project Scope and Feasibility**  
The project is scoped to be achievable for one person within the course timeline. Each part is independent enough to be developed and tested separately, reducing risk and ensuring steady progress.  

The chosen technologies — FastAPI, React, PostgreSQL, and Kubernetes — are lightweight, well-documented, and compatible with each other. With approximately 30 hours of focused work, it is realistic to complete all core features and at least two advanced ones while leaving time for testing and reporting. The design also allows future expansion, such as email alerts or AI-based anomaly detection, without increasing complexity now.

---

## **3. Tentative Plan**  

Since I am completing this project individually, I will handle all stages of development myself. The work will be organized into four main phases, each building on the previous one to ensure steady progress from setup to final deployment and documentation. This approach makes the process manageable and allows each component to be developed and tested independently before full integration.  

**Phase 1 – Local Development:**  
Set up Docker Compose, build the FastAPI backend, define the PostgreSQL schema, and create a basic React frontend to verify full-stack functionality.  

**Phase 2 – Cloud Deployment:**  
Deploy the application to DigitalOcean Kubernetes (DOKS). Write the configuration files for Kubernetes to manage containers, data storage, and internal communication. Verify stability in the cloud.  

**Phase 3 – Monitoring and Automation:**  
Integrate Prometheus and Grafana dashboards, use DigitalOcean metrics, and configure a CI/CD pipeline with GitHub Actions to automate deployment updates.  

**Phase 4 – Security and Documentation:**  
Implement JWT authentication and HTTPS, test the entire system, and prepare the final documentation with screenshots and architecture diagrams.  

By following this plan, I can ensure the system is fully functional, secure, and deployed on time. Each phase produces a working component, which keeps progress visible and manageable throughout the development process.

---

## **References**  

- ECE1779 Course Project Handout – University of Toronto, Department of Electrical & Computer Engineering.  
  [https://www.eecg.utoronto.ca/~cying/courses/ece1779-cloud/project/handout](https://www.eecg.utoronto.ca/~cying/courses/ece1779-cloud/project/handout)  
- FastAPI Documentation – Official documentation for building APIs with Python.  
  [https://fastapi.tiangolo.com](https://fastapi.tiangolo.com)  
- DigitalOcean Kubernetes (DOKS) Documentation – Guides and best practices for deploying containerized applications.  
  [https://docs.digitalocean.com/products/kubernetes/](https://docs.digitalocean.com/products/kubernetes/)  
- Grafana and Prometheus Helm Charts – Community charts for monitoring and observability.  
  [https://github.com/prometheus-community/helm-charts](https://github.com/prometheus-community/helm-charts)  
- GitHub Actions for DigitalOcean Deployments – Reference for CI/CD automation.  
  [https://docs.digitalocean.com/reference/doctl/](https://docs.digitalocean.com/reference/doctl/)
