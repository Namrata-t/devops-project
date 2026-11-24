# DevOps Project: Containerized Flask App

An end-to-end DevOps project: a Flask web app containerized with Docker, built and published by github Actions, deployed on 
Kubernetes (MiniKube), with AWS infrastructure defined in Terraform.

## Architecture

Code -> GitHub -> GitHub Actions -> Docker Hub -> Kubernetes (Minikube) -> Terraform -> AWS EC2 (Free Tier)

## Tech Stack

- App: Python 3.12, Flask
- Containers: Docker
- CI/CD: GitHub Actions (build and push on every push to main)
- Orchestration: Kubernetes via Minikube (Deployment, NodePort Service, probes)
- IaC: Terraform (EC2 t3.micro and Security Group)

## Project Structure

- app.py, requirements.txt: the Flask application
- Dockerfile: container image defination
- .github/workflows/ci.yml: CI pipeline
- k8s/: Kubernetes manifests
- terraform/: AWS infrastructure code

## Run Locally with Docker

	docker build -t devops-flask-app:1.0.0 .
	docker run -d -p 8080:5000 devops-flask-app:1.0.0
	curl http://localhost:8080/health

## Deploy to Kubernetes

	minikube start --driver=docker
	kubectl apply -f k8s/
	minikube service flask-service --url

## Provision AWS Infrastructure

	cd terraform
	terraform init
	terraform plan
	terraform apply
	terraform destroy # always clean up

## What I learned 

- Debugged real pipeline failures (YAML syntax, image naming, secrets)
- Practiced rolling updates, rollbacks, and self-healing in Kubernetes
- Used Terraform plan/apply/destroy with least-privilege IAM and billing guardrails 
