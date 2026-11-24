\# Deployment Documentation



\## Infrastructure



| Component | Configuration |

|---|---|

| Hosting provider | Netcup |

| Operating system | Debian 13 (Trixie) |

| Web server | Nginx |

| Application type | Static web application |

| SSH port | TCP 22 |

| Web root | `/var/www/html/` |

| Version control | Git and GitHub |

| CI/CD platform | GitHub Actions |

| Authentication | SSH key |



\## Architecture



```text

Developer PC (Windows)

&#x20;       |

&#x20;       | Git Push / HTTPS

&#x20;       v

GitHub Repository

&#x20;       |

&#x20;       | Workflow Trigger

&#x20;       v

GitHub Actions (Ubuntu Runner)

&#x20;       |

&#x20;       | SSH / SCP (TCP 22)

&#x20;       v

Netcup VPS (Debian 13)

&#x20;       |

&#x20;       v

Nginx Web Server

&#x20;       |

&#x20;       v

/var/www/html/index.html

```



\## Application Architecture



The application consists of a static HTML file containing HTML, CSS and JavaScript.



All subnet calculations are performed locally in the user's browser. No backend or database is required.



Nginx is responsible for serving the application to the client.



\## Deployment Process



The deployment workflow is located in `.github/workflows/deploy.yml`.



When enabled, the workflow performs the following steps:



1\. Detects a push to the main branch.

2\. Starts a GitHub Actions Ubuntu runner.

3\. Checks out the repository.

4\. Connects to the remote server using SSH.

5\. Creates a timestamped backup of the existing HTML file, if present.

6\. Transfers the updated `index.html` to the server using SCP.

7\. Nginx serves the updated application.



\## Authentication and Secrets



SSH key-based authentication is used for automated deployment.



Connection details are stored in GitHub Actions Secrets:



\- `SERVER\_HOST`

\- `SERVER\_USER`

\- `SSH\_PRIVATE\_KEY`



Secret values are not stored directly in the source code.



\## Backup and Recovery



Before deployment, the existing application file is copied to a timestamped backup.



Previous versions can be restored manually if necessary.



Git also provides version history for the application source code.



\## Known Limitations



\- No automated tests before deployment.

\- No automatic rollback mechanism.

\- Backup files are stored inside the web root.

\- SSH host fingerprint verification is not explicitly configured in the workflow.



\## Current Status



\- Application: Functional

\- Hosting infrastructure: Available

\- Public website: Disabled

\- Automated deployment: Disabled



\## Learning Objectives



\- Linux server administration

\- Static website hosting with Nginx

\- Git version control

\- GitHub Actions

\- Deployment automation

\- SSH and SCP

\- Credential management

\- Backup and recovery



The infrastructure and deployment workflow were configured with AI assistance as part of a practical learning project.

