# 🛠️ SDLC & Architecture Styles

## 🔹 SDLC (Software Development Life Cycle)

- SDLC is the **process of building software systematically** — from idea to deployment & maintenance.
- Common phases: **Requirement → Design → Development → Testing → Deployment → Maintenance**.
- Purpose: Ensures **quality, predictability, and maintainability** of software.

---

## 🔹 Monolith vs Microservices

### 🏗️ Monolith

- **Single codebase** (all features in one repo).
- Easy to build for **small projects**.
- **Slower dev speed** (many devs touching same repo).
- **Scaling is hard** (must scale entire app, not a part).
- **Deployment is tough** (one small change = redeploy whole app).
- **Fault isolation is weak** (one bug can crash everything).
- **Testing is easier** (single codebase).
- **Debugging is easier** (logs in one place).
- **Lower infra cost** for small apps.
- Best for: **Startups / MVPs / Small teams**.

---

### 🧩 Microservices

- **Multiple repos** (each service independent).
- **Faster dev speed** (teams own different services).
- **Scalable** (scale only the service needed).
- **Deployment is easy** (deploy independently).
- Can use **different tech stacks** per service.
- **Better fault isolation** (one service down ≠ full app down).
- **Testing is harder** (E2E testing across many services).
- **Debugging is harder** (distributed logs).
- **Infra cost is higher**.
- Easier **maintenance & ownership** (teams handle their own services).
- Best for: **Large apps, big teams, long-term projects**.

---

## 🔹 Quick Comparison

| Factor          | Monolith                  | Microservices            |
| --------------- | ------------------------- | ------------------------ |
| Dev Speed       | Slower                    | Faster                   |
| Code Repo       | Single                    | Multiple                 |
| Scalability     | Poor                      | Great                    |
| Deployment      | Tough                     | Easy                     |
| Tech Stack      | Mostly same               | Can be different per svc |
| Infra Cost      | Lower                     | Higher                   |
| Complexity      | Simple (small apps)       | Complex (large apps)     |
| Fault Isolation | Weak (whole app affected) | Strong (isolated)        |
| Testing         | Easier                    | Tougher (E2E)            |
| Debugging       | Easier                    | Harder                   |
| Maintenance     | Harder (big codebase)     | Easier (modular)         |
| Ownership       | Centralized               | Decentralized            |

---

## 🔹 Example: DevTinder Project

- We’ll build with **2 microservices**:
  - **Frontend** → React
  - **Backend** → Node.js
