# Go - Orange Belt Projects

Choose **ONE** project as your capstone.

---

## Project 1: Concurrent Web Scraper

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: Goroutines, channels, and HTTP clients

### Description

Build a concurrent web scraper that fetches and processes multiple web pages efficiently using goroutines and channels.

### Requirements

**Core Functionality**:

- [ ] Concurrent fetching of multiple URLs
- [ ] Worker pool pattern for controlled concurrency
- [ ] Rate limiting to be respectful to servers
- [ ] Parse HTML and extract data (use goquery or html package)
- [ ] Store results in structured format (JSON/CSV)
- [ ] Handle errors gracefully (retries, timeouts)

**Advanced Features**:

- [ ] Context for cancellation and timeouts
- [ ] Progress tracking and reporting
- [ ] Duplicate URL detection
- [ ] Robots.txt compliance
- [ ] Configurable concurrency level
- [ ] Resume capability (checkpoint/restore)

**Technical Requirements**:

- [ ] Use channels for communication
- [ ] Implement worker pool with configurable workers
- [ ] Proper resource cleanup (context, HTTP connections)
- [ ] No race conditions (test with `-race`)
- [ ] Comprehensive error handling

**Testing & Quality**:

- [ ] Unit tests for core functions
- [ ] Integration tests with mock HTTP server
- [ ] Benchmarks for performance-critical code
- [ ] Test coverage > 70%

### Deliverables

- [ ] Working scraper with CLI interface
- [ ] Configuration file support
- [ ] README with usage examples
- [ ] Test suite
- [ ] Performance report (pages/second, memory usage)

### Evaluation Criteria

- **Concurrency (35%)**: Proper use of goroutines and channels
- **Functionality (30%)**: All features working correctly
- **Code Quality (20%)**: Clean, idiomatic Go code
- **Testing (15%)**: Comprehensive test coverage

---

## Project 2: REST API with Database

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: HTTP servers, database operations, and testing

### Description

Build a production-ready REST API for a blog or todo application with database persistence, authentication, and proper testing.

### Requirements

**API Endpoints**:

- [ ] GET /api/posts - List all posts (with pagination)
- [ ] GET /api/posts/:id - Get single post
- [ ] POST /api/posts - Create post (authenticated)
- [ ] PUT /api/posts/:id - Update post (authenticated)
- [ ] DELETE /api/posts/:id - Delete post (authenticated)
- [ ] POST /api/auth/login - User authentication
- [ ] POST /api/auth/register - User registration

**Features**:

- [ ] PostgreSQL or MySQL database
- [ ] JWT-based authentication
- [ ] Request validation
- [ ] Proper error responses (with status codes)
- [ ] Middleware (logging, CORS, authentication)
- [ ] Database migrations
- [ ] Environment-based configuration

**Technical Requirements**:

- [ ] Use standard library or popular router (gorilla/mux, chi)
- [ ] Connection pooling for database
- [ ] Prepared statements for SQL
- [ ] Graceful shutdown
- [ ] Request context for cancellation
- [ ] Structured logging

**Testing**:

- [ ] Unit tests for handlers
- [ ] Integration tests with test database
- [ ] Test coverage > 80%
- [ ] API documentation (OpenAPI/Swagger)

### Deliverables

- [ ] Working API server
- [ ] Database schema and migrations
- [ ] Postman/Thunder Client collection
- [ ] Docker Compose setup
- [ ] README with setup instructions
- [ ] Test suite

### Evaluation Criteria

- **Functionality (30%)**: All endpoints working correctly
- **Architecture (25%)**: Clean separation of concerns
- **Security (20%)**: Proper authentication and validation
- **Testing (15%)**: Comprehensive test coverage
- **Documentation (10%)**: Clear API documentation

---

## Project 3: Task Scheduler with Worker Pools

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐⭐ Advanced  
**Focus**: Advanced concurrency patterns and job queuing

### Description

Build a task scheduler that accepts jobs via API, queues them, and processes them using a pool of workers with priority support and retry logic.

### Requirements

**Core Components**:

- [ ] HTTP API to submit jobs
- [ ] In-memory or Redis-backed job queue
- [ ] Worker pool with configurable size
- [ ] Job priority levels (high, medium, low)
- [ ] Job status tracking (pending, running, completed, failed)
- [ ] Retry logic with exponential backoff
- [ ] Job timeout handling

**Job Types** (implement at least 3):

- [ ] HTTP webhook caller
- [ ] Email sender
- [ ] Image processor (resize, compress)
- [ ] Data import/export
- [ ] Report generator

**Advanced Features**:

- [ ] Scheduled jobs (cron-like)
- [ ] Job dependencies (job B runs after job A)
- [ ] Dead letter queue for failed jobs
- [ ] Worker health monitoring
- [ ] Metrics and monitoring (Prometheus)
- [ ] Graceful shutdown (finish in-progress jobs)

**Persistence**:

- [ ] Job metadata in database
- [ ] Job results storage
- [ ] Job history and logs

**API Endpoints**:

- [ ] POST /api/jobs - Submit new job
- [ ] GET /api/jobs/:id - Get job status
- [ ] GET /api/jobs - List jobs (with filters)
- [ ] DELETE /api/jobs/:id - Cancel job
- [ ] GET /api/metrics - Worker and queue metrics

### Deliverables

- [ ] Working scheduler system
- [ ] CLI for job management
- [ ] Monitoring dashboard or metrics endpoint
- [ ] Docker Compose setup
- [ ] Load testing results
- [ ] Complete documentation

### Evaluation Criteria

- **Architecture (30%)**: Well-designed concurrent system
- **Reliability (25%)**: Proper error handling and retries
- **Performance (20%)**: Efficient job processing
- **Features (15%)**: Comprehensive feature set
- **Testing (10%)**: Thorough testing strategy

---

## Project 4: CLI Tool for Cloud Storage

**Time**: 2-3 weeks  
**Difficulty**: ⭐⭐⭐ Intermediate  
**Focus**: File I/O, HTTP, and CLI design

### Description

Build a command-line tool for uploading, downloading, and managing files in cloud storage (S3, Google Cloud Storage, or similar).

### Requirements

**Commands**:

- [ ] `upload <file> <bucket>` - Upload file
- [ ] `download <file> <bucket>` - Download file
- [ ] `list <bucket>` - List files
- [ ] `delete <file> <bucket>` - Delete file
- [ ] `sync <local-dir> <bucket>` - Sync directory
- [ ] `config` - Configure credentials

**Features**:

- [ ] Concurrent uploads/downloads
- [ ] Progress bar for large files
- [ ] Resume capability for interrupted transfers
- [ ] Checksum verification
- [ ] Compression before upload (optional)
- [ ] Encryption support (optional)
- [ ] Filter files by pattern (glob)

**Technical Requirements**:

- [ ] Use cobra or flag for CLI
- [ ] Configuration file support
- [ ] Proper error messages
- [ ] Logging with levels (debug, info, error)
- [ ] Cross-platform compatibility

**Testing**:

- [ ] Unit tests with mocked cloud storage
- [ ] Integration tests with local S3 (MinIO)
- [ ] Test large file handling
- [ ] Test concurrent operations

### Deliverables

- [ ] Working CLI tool
- [ ] Installation instructions (or release binaries)
- [ ] User documentation
- [ ] Test suite
- [ ] Demo video or GIF

### Evaluation Criteria

- **Usability (30%)**: Intuitive CLI interface
- **Functionality (30%)**: All features working correctly
- **Performance (20%)**: Efficient file operations
- **Code Quality (10%)**: Clean, maintainable code
- **Documentation (10%)**: Clear user docs

---

Choose one project that excites you and demonstrates your Go skills!
