# 

---

#  readme file


```markdown
# Air Traffic Control System Simulator
A POSIX-compliant multi-process system simulating real-time air traffic management with concurrent plane/airport operations and IPC synchronization.

## 🛠️ Implementation Highlights
- **Multi-process Architecture**: 4 independent programs (`plane`, `airport`, `airtrafficcontroller`, `cleanup`) with 1500+ LOC
- **Complex IPC**: Single message queue handles 4+ message types with priority routing
- **Synchronization**: Semaphore-controlled runway allocation with best-fit algorithm
- **Weight Calculations**: Passenger/cargo load management with pipe-based child processes
- **Graceful Termination**: System-wide cleanup handling pending operations

## 📁 Core Components
| File | Description | Key Features |
|------|-------------|--------------|
| `plane.c` | Aircraft process manager | Parent-child passenger hierarchy, Dual plane types, Pipe-based IPC |
| `airport.c` | Airport operations | Multi-threaded runway management, Best-fit allocation, Synchronized landings/takeoffs |
| `airtrafficcontroller.c` | Central coordinator | Message queue routing, Journey logging, System orchestration |
| `cleanup.c` | Termination handler | Safe system shutdown protocol |

## 🚀 Quick Start
```


# Compile all components

gcc plane.c -o plane
gcc airport.c -o airport -pthread
gcc airtrafficcontroller.c -o atc
gcc cleanup.c -o cleanup

# Run system (in separate terminals)

./atc        \# Start controller first
./airport    \# Run N instances (matches airport count)
./plane      \# Start aircraft processes
./cleanup    \# For graceful shutdown

```

## 🔗 Operational Workflow
1. **Controller Initialization**: Creates message queue and manages airport count
2. **Airport Setup**: Configures runways (including 15,000kg emergency runway)
3. **Plane Lifecycle**:
   - Passenger/Cargo type selection
   - Weight calculation (passengers: 7 crew + luggage | cargo: 2 crew + items)
   - Route planning (departure/arrival airports)
4. **ATC Coordination**: Routes messages between airports/planes
5. **Runway Operations**: Thread-based best-fit allocation with semaphore locking

## ⚙️ Technical Specifications
- **IPC**: Single System V message queue (4 message types)
- **Synchronization**: POSIX semaphores for runway access
- **Logging**: Real-time updates in `AirTrafficController.txt`
- **Constraints**: 
  - Max 10 airports with 10 runways each
  - 10,000-12,000kg runway capacity (+15,000kg emergency)
  - 30s flight duration simulation

> **Note**: Developed for Ubuntu 22.04 LTS with strict POSIX compliance
```

