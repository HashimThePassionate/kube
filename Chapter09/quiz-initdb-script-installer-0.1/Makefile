# ==========================================
# Configuration Variables
# ==========================================
REGISTRY ?= muhammadhashim24
IMAGE_NAME ?= quiz-initdb-script-installer
TAG ?= 0.1
FULL_IMAGE = $(REGISTRY)/$(IMAGE_NAME):$(TAG)

# ==========================================
# Default Target (Ab sirf 'make' likhne par build + kind-load dono honge)
# ==========================================
all: kind-load

# ==========================================
# Rules & Tasks
# ==========================================

# 1. Docker image build karne ka rule
build: Dockerfile
	@echo "----------------------------------------"
	@echo "Building Docker image: $(FULL_IMAGE)"
	@echo "----------------------------------------"
	docker build -t $(FULL_IMAGE) .

# 2. Docker Hub par push karne ka rule
push: build
	@echo "----------------------------------------"
	@echo "Pushing $(FULL_IMAGE) to Docker Hub..."
	@echo "----------------------------------------"
	docker push $(FULL_IMAGE)

# 3. Local Kind (Kubernetes) cluster mein load karne ka rule (Yeh 'build' par depend karta hai)
kind-load: build
	@echo "----------------------------------------"
	@echo "Loading image into local Kind cluster..."
	@echo "----------------------------------------"
	kind load docker-image $(FULL_IMAGE)

# 4. Local cleanup ka target
clean:
	@echo "----------------------------------------"
	@echo "Cleaning up local Docker image..."
	@echo "----------------------------------------"
	docker rmi -f $(FULL_IMAGE) || true