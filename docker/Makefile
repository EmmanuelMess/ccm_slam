all: help

CATKIN_WS=/root/ccmslam_ws
PROJECT_ROOT = ${PWD}/../..
PROJECT_SOURCE = ${PWD}/..
DOCKER_RUN = docker run --rm --volume "$(PROJECT_SOURCE):$(CATKIN_WS)/src/ccm_slam" --volume "$(PROJECT_ROOT)/build:$(CATKIN_WS)/build" --volume "$(PROJECT_ROOT)/devel:$(CATKIN_WS)/devel" --volume "$(PROJECT_ROOT)/install:$(CATKIN_WS)/install" --volume "$(PROJECT_ROOT)/logs:$(CATKIN_WS)/logs"

help:
	@echo ""
	@echo "-- Help Menu"
	@echo ""
	@echo "   1. make build              - build docker image"
	@echo "   1. make clean              - remove all images"
	@echo ""

build:
	echo "Use -j$(NR_JOBS) for build commands"
	docker build --tag ccm_slam -f ./Dockerfile --build-arg NR_JOBS=$(NR_JOBS) ..
	$(DOCKER_RUN) --workdir "$(CATKIN_WS)/src/ccm_slam/cslam/thirdparty/DBoW2/" ccm_slam /bin/bash -c "mkdir -p build; cd build; cmake ..; make -j$(NR_JOBS)"
	$(DOCKER_RUN) --workdir "$(CATKIN_WS)/src/ccm_slam/cslam/thirdparty/g2o/" ccm_slam /bin/bash -c "mkdir -p build; cd build; cmake --cmake-args -DG2O_U14=0 ..; make -j$(NR_JOBS)"
	$(DOCKER_RUN) --workdir "$(CATKIN_WS)/src/ccm_slam/cslam/conf" ccm_slam /bin/bash -c "unzip -n ORBvoc.txt.zip"
	$(DOCKER_RUN) --workdir "$(CATKIN_WS)" ccm_slam /bin/bash -c "catkin build ccmslam --cmake-args -DG2O_U14=0 -DCMAKE_BUILD_TYPE=Release"

clean:
	docker rmi -f ccm_slam
