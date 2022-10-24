```mermaid
sequenceDiagram
    participant SWARM 
    participant GitHub Workflow
    participant p4_setup
    participant test_cppcheck
    participant comment
    participant P4
    SWARM->>GitHub Workflow: review, change, update
    GitHub Workflow->>p4_setup: change, PORT,USER,PASSWD
    p4_setup->>GitHub Workflow: files
    GitHub Workflow->>test_cppcheck:./temp
    test_cppcheck->>GitHub Workflow: result_cppcheck.txt
    GitHub Worflow->>comment:update,review,result_cppcheck.txt
    comment->>SWARM: comment
```
