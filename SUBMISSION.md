# PA4 Submission: TaskFlow Pipeline

## Student Information

| Field | Value |
|---|---|
| Name | Muhammadjon Raza |
| Roll Number | 27100293 |
| GitHub Repository URL | `https://github.com/0x0shephard/CS487-PA4` |
| Resource Group | `rg-sp26-27100293` |
| Assigned Region | `ukwest` |

## Task 1: App Service Web App

### Evidence 1.1: Forked Repository

![Forked repository](docs/01-forked-repo.png)

This screenshot shows the working GitHub fork that contains the PA4 starter structure and submitted implementation files.

### Evidence 1.2: App Service Overview

![Web App running status](docs/02-web-app-running-status.png)

This screenshot shows the App Service Web App `pa4-27100293` in the assigned resource group and region with a running public endpoint.

### Evidence 1.3: Deployment Center / GitHub Actions

![GitHub deployment configuration](docs/03-github-configuration.png)

This screenshot shows the GitHub deployment wiring used for the App Service deployment.

### Evidence 1.4: Application Settings and Live UI

![Web app application settings](docs/04-application-settings-configured.png)

The Web App is configured with the Durable Function starter and status URLs.

![Dashboard loaded in browser](docs/05-dashboard-loading-in-a-browser.png)

This screenshot confirms the TaskFlow dashboard loads from the live App Service URL.

## Task 2: Azure Container Registry

### Evidence 2.1: ACR Overview

![ACR overview](docs/06-acr.png)

This screenshot shows the Azure Container Registry used to store all TaskFlow container images.

### Evidence 2.2: AKS Resource and Docker Builds

![AKS overview](docs/07-aks.png)

This screenshot shows the AKS resource used for the validator service.

![Docker builds](docs/08-docker-builds-for-all-three-images.png)

This screenshot shows local Docker builds for the three images: `validate-api`, `report-job`, and `func-app`.

### Evidence 2.3: Local Validator Test, Pushes, and ACR Repositories

![Local validator test](docs/09-local-test-of-the-validator-post-validate-returning-js.png)

The validator API was tested locally with a `POST /validate` request that returned JSON.

![Docker pushes](docs/10-successful-pushes-to-acr-for-all-three-images.png)

This screenshot shows successful pushes to ACR for the required images.

![ACR repository list](docs/11-acr-repository-list-showing-validate-api-report-job-an.png)

This screenshot confirms that `validate-api`, `report-job`, and `func-app` repositories exist in ACR.

## Task 3: Durable Function Implementation

### Evidence 3.1: Completed Function Code

[function_app.py](function-app/function_app.py)

The Durable Function defines an HTTP starter, `my_orchestrator`, `validate_activity`, and `report_activity`. The orchestrator first validates the order through AKS and only creates the ACI report job when validation succeeds.

### Evidence 3.2: Local Function Handler Listing

![Function handlers registered](docs/12-func-start-showing-all-four-durable-handlers-registere.png)

This screenshot shows the Durable Functions runtime discovering all four handlers locally.

## Task 4: Function App Container Deployment

### Evidence 4.1: Function App Container Configuration

![Function App container configuration 1](docs/13-function-app-in-azure-portal-showing-the-container-ima.png)

![Function App container configuration 2](docs/14-function-app-in-azure-portal-showing-the-container-ima.png)

![Function App container configuration 3](docs/15-function-app-in-azure-portal-showing-the-container-ima.png)

![Function App container configuration 4](docs/16-function-app-in-azure-portal-showing-the-container-ima.png)

These screenshots show the Function App container configuration and the ACR-hosted `func-app:v1` image.

### Evidence 4.2: Orchestration Smoke Test

![Curl orchestration starter output](docs/17-curl-output-showing-the-orchestration-started-instance.png)

This screenshot shows the HTTP starter returning an orchestration `id` and `statusQueryGetUri`, proving the Function App accepted a Durable orchestration request.

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Expected failed status before wiring](docs/18-status-query-url-json-showing-failed-status-at-this-st.png)

This screenshot shows the expected early failure before all downstream settings were wired.

## Task 5: AKS Validator

### Evidence 5.1: Kubernetes Nodes and Pods

![kubectl get nodes](docs/19-kubectl-get-nodes-showing-your-cluster-is-running.png)

The AKS node is running and available.

![kubectl get pods](docs/20-kubectl-get-pods-showing-the-validator-pod-is-running.png)

The validator pod is scheduled and running.

### Evidence 5.2: Kubernetes Service

![kubectl get service](docs/21-kubectl-get-service-showing-the-assigned-external-ip.png)

The validator service is exposed with a LoadBalancer external IP on port `8080`.

### Evidence 5.3: Validator API Tests

![Validator curl tests](docs/22-curl-health-and-both-curl-validate-runs.png)

This screenshot shows `/health`, a valid `/validate` request, and an invalid quantity request.

### Evidence 5.4: Function App `VALIDATE_URL`

![Function App VALIDATE_URL setting](docs/23-function-app-application-setting-validate-url.png)

The Function App uses `VALIDATE_URL` to call the AKS-hosted validation endpoint.

## Task 6: ACI Report Job

### Evidence 6.1: Blob Container and Manual ACI Run

![Task 6 evidence 1](docs/24-task-6.png)

![Task 6 evidence 2](docs/25-task-6.png)

![Task 6 evidence 3](docs/26-task-6.png)

These screenshots show the report container and manual ACI report-job evidence.

### Evidence 6.2: ACI Logs and Generated PDF

![Task 6 evidence 4](docs/27-task-6.png)

![Task 6 evidence 5](docs/28-task-6.png)

These screenshots show the report-job execution and generated PDF evidence.

### Evidence 6.3: Function App Identity and Report Settings

![Task 6 evidence 6](docs/29-task-6.png)

![Task 6 evidence 7](docs/30-task-6.png)

These screenshots show the Function App identity and report-related app settings used to create ACI jobs and upload PDFs.

## Task 7: End-to-End Pipeline

### Evidence 7.1: Web App Wiring

![Web app Function URL settings](docs/32-task-8.png)

This screenshot shows `FUNCTION_START_URL` and `FUNCTION_STATUS_URL` configured on the Web App.

### Evidence 7.2: Happy Path UI

![Happy path UI 1](docs/33-four-happy-path-screenshots-from-step-7-2.png)

![Happy path UI 2](docs/34-four-happy-path-screenshots-from-step-7-2.png)

![Happy path UI 3](docs/35-four-happy-path-screenshots-from-step-7-2.png)

These screenshots show the valid order flow progressing through the TaskFlow UI to a completed report.

### Evidence 7.3: Backend Participation

![Blob container overview](docs/31-task-8.png)

This screenshot shows the `reports` blob container with generated report PDFs.

![Blob report PDF evidence](docs/36-the-blob-container-showing-the-new-pdf-matching-your-o.png)

The `reports` container contains a generated PDF matching an end-to-end order ID.

![Downloaded PDF open in viewer](docs/37-the-downloaded-pdf-open-in-a-viewer.png)

This screenshot shows the downloaded report PDF opened locally, proving the ACI-generated artifact is a usable PDF.

![Function monitor invocation 1](docs/38-function-app-monitor-invocations-showing-the-orchestra.png)

![Function monitor invocation 2](docs/39-function-app-monitor-invocations-showing-the-orchestra.png)

![Function monitor invocation 3](docs/40-function-app-monitor-invocations-showing-the-orchestra.png)

![Function monitor invocation 4](docs/41-function-app-monitor-invocations-showing-the-orchestra.png)

These screenshots show Function App invocation evidence for the starter, orchestrator, and activities.

![AKS validator traffic 1](docs/42-aks-pod-logs-or-aks-metrics-showing-the-validator-rece.png)

![AKS validator traffic 2](docs/43-aks-pod-logs-or-aks-metrics-showing-the-validator-rece.png)

![AKS validator traffic 3](docs/44-aks-pod-logs-or-aks-metrics-showing-the-validator-rece.png)

These screenshots show AKS pod logs and metrics proving the validator received traffic during the run.

![Resource group overview](docs/45-resource-group-picture.png)

This screenshot shows the deployed resource group resources used by the full pipeline.

### Evidence 7.4: Reject Path UI

![Reject flow UI](docs/46-rejection-flow.png)

![Reject flow durable status](docs/47-rejection-flow.png)

These screenshots show an order rejected because quantity exceeded the validator rule.

![Reject orchestration evidence 1](docs/48-i-am-unable-to-get-the-function-app-monitor-showing-th.png)

![Reject orchestration evidence 2](docs/49-i-am-unable-to-get-the-function-app-monitor-showing-th.png)

The Portal monitor showed successful function execution, while the Durable status query showed the business output as rejected. This is expected because the orchestration completed normally but returned `{"status":"rejected","reason":"quantity exceeds limit"}` instead of spawning a report ACI.

## Task 8: Write-Up and Architecture Diagram

### Evidence 8.1: Architecture Diagram

Mermaid source file: [docs/architecture.mmd](docs/architecture.mmd)

```mermaid
flowchart TD
    user[User Browser]
    github[GitHub Fork + Actions]
    web[Azure App Service Web App<br/>pa4-27100293]
    func[Azure Durable Functions<br/>pa4-func-27100293]
    orch[my_orchestrator]
    validate[AKS validate-api<br/>validate-service :8080]
    aci[Azure Container Instance<br/>ci-report-&lt;order_id&gt;]
    blob[Blob Storage<br/>reports container]
    acr[Azure Container Registry<br/>validate-api, report-job, func-app]
    mi[Managed Identity<br/>mi-pa4-27100293]

    github -->|deploys web app| web
    github -->|container images| acr
    acr -->|validate-api:v1| validate
    acr -->|func-app:v1| func
    acr -->|report-job:v1| aci
    user -->|submit order| web
    web -->|HTTP starter| func
    func --> orch
    orch -->|validate_activity| validate
    orch -->|report_activity creates job| aci
    aci -->|uploads PDF| blob
    web -->|poll status URL| func
    func -->|returns report URL or rejected status| web
    mi -->|RBAC for storage, ACI creation, blob upload| func
    mi -->|attached to report ACI| aci
```

## 10.1 Report Requirements

### 1. Service Selection

**App Service.** App Service is the right fit for the TaskFlow web front end because it runs a long-lived HTTP application with minimal infrastructure management. The Node/Express web app needs a stable public URL, environment variables, HTTPS, and GitHub deployment integration, all of which App Service provides directly. Its cost model is predictable because the App Service Plan stays allocated, which is reasonable for a small always-available dashboard. It also scales horizontally if the UI/proxy receives more traffic, without requiring container orchestration.

**Durable Functions.** Durable Functions is the right tool for the order workflow because the process is stateful: it starts with validation, conditionally runs report generation, and exposes status polling while the work continues. A report job can take tens of seconds, so the web request should not block until the full pipeline finishes. Durable Functions persists orchestration state in storage and provides a standard status URL, which makes retries, replay, and completion tracking easier than plain HTTP handlers. It is also cost-efficient for workflow control because it only runs when work is triggered.

**Azure Kubernetes Service.** AKS is appropriate for the validator because it represents a continuously available microservice that may receive many validation requests. A pod and LoadBalancer service keep the validator ready for low-latency calls from the Function App. AKS has more operational overhead and baseline cost than serverless options, but it gives control over container deployment, scaling, and service networking. For a real shared validation service, the always-on model can be justified because many orders can reuse the same running pods.

**Azure Container Instances.** ACI is the right fit for report generation because each report is a short-lived one-shot container job. The report worker does not need to stay running while idle, so creating an ACI per accepted order avoids paying for a dedicated report service. ACI has a simple operational model: the Function App creates a container group, waits for completion, and deletes it after the PDF is uploaded. This model keeps report generation isolated and scales by creating independent containers for independent report jobs.

### 2. ACI vs. AKS: Hands-On Comparison

When AKS is idle for 10 minutes, the cluster and node still exist and continue running unless explicitly stopped or scaled down. The validator pod remains scheduled, and metrics still show CPU and memory usage even when there are no order requests. In this pipeline, idle AKS means no current validation traffic, not zero cost; the node pool still consumes compute because it is ready to receive traffic at any time.

For ACI, idle means there is no report container group running. The pipeline creates ACI only during `report_activity`, and then the Function deletes the container group after the PDF upload. That means ACI does not keep an idle worker around between orders; cost is tied to the short window when each report container exists.

If a malicious user spammed Submit 1000 times in a minute with valid orders, ACI would likely create the largest burst cost because each accepted order can spawn a separate report container. AKS would also see validation load, but the validator runs on already allocated nodes unless scaling adds more nodes. Durable Functions would incur execution/storage operations, but the expensive part would be many report containers running concurrently. If the spammed orders were invalid, ACI cost would be avoided because rejected orders do not spawn report jobs.

### 3. Durable Functions: Why Not Just HTTP?

Implementing the same flow as two plain HTTP-triggered functions would make state and coordination harder. The web app would need to remember whether validation succeeded, whether a report job had started, and how to recover if the report step timed out or failed halfway through. Function timeouts and client HTTP timeouts would be a problem because report generation can take up to a minute, while Durable Functions lets the client poll status asynchronously. Durable Functions also provides persisted orchestration state and replay semantics, which are useful for retry-on-failure and for returning a final completed or rejected result without losing progress.

### 4. Cost Review

Cost Management should be captured from Azure Portal using **Cost Management -> Cost Analysis** scoped to `rg-sp26-27100293`. For this PA, the total cost should be low because the workload is small and short-lived. The single most expensive resource is expected to be AKS, because its node pool continues running even when no validation requests are being processed. App Service also has a baseline cost from the App Service Plan, while ACI, Storage, ACR, and Functions are comparatively small for this assignment-sized workload.

The Cost Analysis screenshot was not present in `Screenshots.docx`; add it under this section if your instructor requires the visual evidence in addition to the written cost estimate.

### 5. Challenges Faced

One issue was that the Function App host returned `Function host is not running`. Runtime logs showed `AuthorizationFailure` while the Functions host tried to access Blob Storage for host secrets. The cause was storage network/security configuration, not the application code. Enabling a valid network path to the storage account while keeping managed identity authentication fixed the host startup.

Another issue was that the AKS validator endpoint stopped responding during end-to-end testing. Checking `az aks show` revealed that the AKS cluster was stopped, which explained both the dead LoadBalancer endpoint and the Function validation timeout. Starting AKS again, refreshing kube credentials, and retesting `/health` and `/validate` restored the validator path.

A third issue was the transient nature of ACI evidence. The report container group is intentionally deleted after the PDF upload, so `az container list` only shows it briefly. To prove ACI participation, I captured the container while it was running and also used Azure Activity Log entries showing `containerGroups/write` followed by `containerGroups/delete` for `ci-report-<order_id>`.
