# COWORKING SPACE SERVICE DEPLOYMENT GUIDE

The **Coworking Space Service** consists of APIs for users to request tokens and admins to manage coworking space access. This guide helps set up a pipeline to deploy the API for basic user activity analytics in Kubernetes.

---

## **REQUIREMENTS**

### **Local Tools**
- **Python 3.6+**: Install dependencies using `pip`.
- **Docker CLI**: Build and test Docker images locally.
- **kubectl**: Manage Kubernetes clusters.
- **Helm**: Deploy Helm charts on Kubernetes.

### **AWS Resources**
- **AWS CodeBuild**: Build Docker images.
- **AWS ECR**: Store Docker images.
- **AWS EKS**: Deploy Kubernetes cluster.
- **AWS CloudWatch**: Monitor logs and metrics.
- **GitHub**: Store and pull code.

---

## **STEPS**

1. **Set up AWS CLI**: Run `aws configure` to configure AWS credentials.
2. **Create ECR Repository**: Store Docker images in Amazon ECR.
3. **Set up CodeBuild**: Connect CodeBuild to GitHub to trigger builds.
4. **Write `buildspec.yaml`**: Define build steps to push images to ECR.
5. **Push Code to GitHub**: Automatically trigger builds in CodeBuild.
6. **Deploy Kubernetes Resources**:
   - Apply configs: `kubectl apply -f configmap.yaml`
   - Deploy app: `kubectl apply -f coworking.yaml`

---

## **SUGGESTIONS**

1. **Reasonable Memory and CPU Allocation**:  
   Allocate sufficient CPU and memory in the Kubernetes deployment to prevent resource bottlenecks. For example, start with `512Mi` memory and `0.5 CPU` per pod for small workloads, then adjust based on performance needs.

2. **Best AWS Instance Type**:  
   Use **t3.medium** instances for a balance of cost and performance for moderate workloads. This instance type is burstable, which makes it suitable for dynamic traffic.

3. **Cost Optimization**:  
   Implement auto-scaling to adjust resources dynamically based on demand. Monitor resource usage with CloudWatch and use reserved instances or spot instances for predictable workloads to save costs.