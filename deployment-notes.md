# LibreChat Deployment Options Guide

## 🏗️ Available Deployment Strategies

LibreChat offers multiple deployment approaches, each optimized for different use cases and environments. Here's a comprehensive analysis of when to use each option.

---

## 1. 📦 **Standard Docker Compose** (`docker-compose.yml`)

### **Architecture:**
- **Single monolithic container** (API + Client)
- Uses pre-built image: `ghcr.io/danny-avila/librechat-dev:latest`
- All-in-one approach with built-in client serving

### **Best For:**
- ✅ **Development & Testing**
- ✅ **Quick local setup**
- ✅ **Small teams (1-10 users)**
- ✅ **Learning LibreChat**

### **Pros:**
- Simple setup - one command to run
- Minimal configuration required
- Fast deployment
- Good for prototyping

### **Cons:**
- No separation of concerns
- Limited scalability
- Single point of failure
- No load balancing capabilities

### **Resource Requirements:**
- **RAM:** 2-4GB
- **CPU:** 2 cores minimum
- **Storage:** 10GB+

---

## 2. 🚀 **Production Docker Compose** (`deploy-compose.yml`)

### **Architecture:**
- **Microservices approach** (API + NGINX + Databases)
- Separate API container: `ghcr.io/danny-avila/librechat-dev-api:latest`
- NGINX reverse proxy for client serving
- Production-optimized configuration

### **Best For:**
- ✅ **Production deployments**
- ✅ **Medium to large teams (10-100+ users)**
- ✅ **Public-facing applications**
- ✅ **SSL/HTTPS requirements**

### **Pros:**
- Proper separation of concerns
- NGINX for static file serving & reverse proxy
- SSL/HTTPS ready configuration
- Better performance and caching
- Horizontal scaling potential
- Production security practices

### **Cons:**
- More complex setup
- Requires SSL certificate management
- More moving parts to monitor

### **Resource Requirements:**
- **RAM:** 4-8GB
- **CPU:** 4+ cores recommended
- **Storage:** 20GB+

---

## 3. 🔧 **Custom Build** (`Dockerfile` vs `Dockerfile.multi`)

### **Dockerfile (Single-stage):**
```dockerfile
# Simple, monolithic build
FROM node:20-alpine AS node
# Builds everything in one container
```

**Best For:**
- Quick custom builds
- Development with custom modifications
- Simple deployment scenarios

### **Dockerfile.multi (Multi-stage):**
```dockerfile
# Optimized, multi-stage build
FROM node:20-alpine AS base-min
# Separate stages for each component
```

**Best For:**
- Production custom builds
- Optimized image sizes
- Complex build requirements
- CI/CD pipelines

### **When to Build Custom:**
- ✅ **Custom code modifications**
- ✅ **Specific dependency versions**
- ✅ **Air-gapped environments**
- ✅ **Security compliance requirements**

---

## 4. ☸️ **Kubernetes/Helm** (`helm/` directory)

### **Architecture:**
- **Cloud-native deployment**
- Kubernetes manifests with Helm charts
- Auto-scaling and high availability
- Enterprise-grade orchestration

### **Best For:**
- ✅ **Enterprise deployments**
- ✅ **Cloud environments (AWS, GCP, Azure)**
- ✅ **High availability requirements**
- ✅ **Auto-scaling needs**
- ✅ **Large organizations (100+ users)**

### **Pros:**
- Auto-scaling and self-healing
- Rolling updates with zero downtime
- Resource management and limits
- Service mesh integration
- Multi-environment support

### **Cons:**
- Complex setup and management
- Requires Kubernetes expertise
- Higher operational overhead
- More expensive infrastructure

### **Resource Requirements:**
- **Cluster:** 3+ nodes minimum
- **RAM:** 8GB+ per node
- **CPU:** 4+ cores per node

---

## 🎯 **Decision Matrix**

| Use Case | Recommended Option | Why |
|----------|-------------------|-----|
| **Learning/Testing** | `docker-compose.yml` | Simple, fast setup |
| **Development Team** | `docker-compose.yml` + overrides | Flexible, customizable |
| **Small Production** | `deploy-compose.yml` | Production-ready, manageable |
| **Enterprise** | Kubernetes/Helm | Scalable, enterprise features |
| **Custom Requirements** | Custom Dockerfile | Full control over build |
| **Air-gapped/Secure** | `Dockerfile.multi` | Optimized, secure builds |

---

## 🔧 **Configuration Files Explained**

### **docker-compose.override.yml**
- Extends base `docker-compose.yml`
- Local development customizations
- Volume mounts for config files
- Environment-specific settings

### **client/nginx.conf**
- NGINX reverse proxy configuration
- SSL/HTTPS setup (commented out by default)
- File upload size limits (25MB)
- Compression and caching rules

### **.env File Requirements**
All deployment methods require:
```bash
# Core settings
PORT=3080
MONGO_URI=mongodb://mongodb:27017/LibreChat
MEILI_MASTER_KEY=your-secret-key

# User permissions (for docker-compose.yml)
UID=501
GID=20

# API Keys (add as needed)
OPENAI_API_KEY=your-key
ANTHROPIC_API_KEY=your-key
```

---

## 🚦 **Migration Path**

### **Development → Production:**
1. Start with `docker-compose.yml`
2. Add `docker-compose.override.yml` for customizations
3. Move to `deploy-compose.yml` for production
4. Consider Kubernetes for scale

### **Local → Cloud:**
1. Test locally with `deploy-compose.yml`
2. Set up SSL certificates
3. Configure domain and DNS
4. Deploy to VPS/cloud instance
5. Scale with Kubernetes if needed

---

## 📊 **Performance Comparison**

| Metric | Standard | Production | Kubernetes |
|--------|----------|------------|------------|
| **Setup Time** | 5 minutes | 30 minutes | 2+ hours |
| **Scalability** | Low | Medium | High |
| **Maintenance** | Low | Medium | High |
| **Performance** | Good | Better | Best |
| **Cost** | Low | Medium | High |

---

## 🔒 **Security Considerations**

### **Development (docker-compose.yml):**
- Uses development images
- Exposed ports for debugging
- Minimal security hardening

### **Production (deploy-compose.yml):**
- Production-optimized images
- NGINX security headers
- SSL/HTTPS ready
- Database access restrictions

### **Enterprise (Kubernetes):**
- Network policies
- RBAC and service accounts
- Secrets management
- Pod security standards

---

## 💡 **Recommendations**

### **For Your Current Setup:**
Given your local development with Ollama and MCP integration:

1. **Continue with `docker-compose.yml`** for development
2. **Use `docker-compose.override.yml`** for your custom configurations
3. **Test with `deploy-compose.yml`** before any production deployment
4. **Consider Kubernetes** only if you need enterprise features

### **Next Steps:**
1. Fix the current logs directory permission issue
2. Test MCP integration stability
3. Add proper SSL certificates for production
4. Set up monitoring and backup strategies

---

*Last updated: September 26, 2025*
*LibreChat Version: v0.8.0-rc4*
