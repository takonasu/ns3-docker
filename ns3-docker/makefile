NAME=docker-ns3-36-1

build: Dockerfile
	if [ -d "./ns-allinone-3.35" ]; then \
		echo "Dir exists, skip downloading .."; \
	else \
		wget https://www.nsnam.org/releases/ns-allinone-3.35.tar.bz2; \
		tar -xf ./ns-allinone-3.35.tar.bz2; \
		rm ./ns-allinone-3.35.tar.bz2; \
	fi
	docker build -t $(NAME) .

run:
	docker run --rm -it -v `pwd`/ns-allinone-3.35/ns-3.35/src/:/usr/ns3/ns-3.35/src -e DISPLAY=docker.for.mac.host.internal:0 $(NAME)