LINKERFLAGS = -X main.Version=`git describe --tags --always --long --dirty` -X main.BuildTimestamp=`date -u '+%Y-%m-%d_%I:%M:%S_UTC'`

.ONESHELL:
build-alpine:
	cd src
	GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -a -o main -ldflags "$(LINKERFLAGS)"

run-docker:
	make build-alpine
	docker-compose up --build

.ONESHELL:
run-dev:
	cd src
	go run . -d postgresql://admin:supersecret@localhost:5432/scrumlr?sslmode=disable

run-docker-dev:
	docker-compose --profile dev up

.ONESHELL:
test:
	cd src
	go test ./... -cover -coverprofile=coverage.txt

.ONESHELL:
coverage:
	make test
	cd src
	go tool cover -html=coverage.txt