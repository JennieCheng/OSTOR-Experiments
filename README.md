# OSTOR: Online Scheduling Framework

OSTOR is a online scheduling framework for data trading, which can be seamlessly integrated into existing stream processing frameworks (such as Apache Flink, Apache Storm, Apache Spark Streaming). It provides efficient resource allocation and query optimization for real-time data streaming workloads while considering budget constraints and system dynamics.

## Key Features

- **Easy Integration**: Can be directly plugged into existing stream processing systems
- **Framework Agnostic**: Compatible with all major stream processing frameworks
- **Adaptive Management**: Dynamically adjusts resource allocation based on workload changes
- **Cost-Effective**: Optimizes resource usage while respecting budget constraints
- **Performance Oriented**: Maintains high throughput and low latency for stream processing

## Supported Frameworks

- Apache Flink
- Apache Storm

## Quick Integration Guide

```java
// For Apache Flink
public class FlinkOSTORIntegration {
    public static void configure(StreamExecutionEnvironment env) {
        // Initialize OSTOR
        OSTORConfig config = new OSTORConfig()
            .setResourceMode(ResourceMode.ADAPTIVE)
            .setMaxParallelism(10);
            
        // Attach OSTOR resource manager
        env.setResourceManager(new OSTORResourceManager(config));
        
        // Enable dynamic scaling
        env.enableDynamicScaling(true);
    }
}

// For Apache Storm
public class StormOSTORIntegration {
    public static void configure(TopologyBuilder builder) {
        // Add OSTOR resource management
        Config conf = new Config();
        conf.put(Config.TOPOLOGY_RAS_MANAGER, 
                "com.ostor.storm.OSTORResourceManager");
                
        // Set adaptive scheduling
        conf.put(Config.TOPOLOGY_SCHEDULER_STRATEGY,
                "com.ostor.storm.OSTORScheduler");
    }
}
```

## System Overview

OSTOR can be integrated into existing stream processing systems like Apache Flink, Apache Storm, or custom stream processing frameworks.

## Code Structure and Implementation Guide

### Core Algorithm Implementation

#### 1. OSTOR Main Algorithm (`ostor.m`)
```matlab
function [sigma, phi, profit, u, d] = ostor(v, b, a, B, flag)
```
- **Purpose**: Main implementation of OSTOR algorithm
- **Key Components**:
  - Dynamic resource allocation
  - Budget tracking
  - Profit calculation
  - Utilization monitoring
- **Parameters**:
  - `v`: Query values vector
  - `b`: Assignment costs matrix
  - `a`: Activation costs vector
  - `B`: Budget constraints
  - `flag`: Operation mode selector

#### 2. Adaptive Dual Descent Algorithm (`adaptive_dual_descent_algorithm.m`)
```matlab
function [sigma, phi, X, Y, U, profit] = adaptive_dual_descent_algorithm(b, a)
```
- **Purpose**: Core optimization algorithm
- **Key Features**:
  - Resource allocation optimization
  - Social welfare maximization
  - Cost minimization
- **Output**:
  - `sigma`: Allocation matrix
  - `phi`: Dual variables
  - `X`, `Y`, `U`: Set partitions
  - `profit`: Achieved profit

#### 3. Query Management Strategies

##### Reactivation Strategy (`reactivate.m`)
```matlab
function [sigma, phi, X, Y, U, profit] = reactivate(b, a, sigma, phi, X, Y, U, profit, tb)
```
- **Purpose**: Implements iterative reactivation strategy (IRS)
- **When to Use**: For handling plans that become profitable

##### Reassignment Strategy (`reassign.m`)
```matlab
function [sigma, phi, X, Y, U, profit] = reassign(b, a, sigma, phi, X, Y, U, profit, tb)
```
- **Purpose**: Implements dynamic reassignment strategy (IRS)
- **When to Use**: For handling queries that become profitable

### Experimental Validation

#### 1. Online Performance Evaluation (`test_online_socialwelfare_exp1.m`)
- Tests system performance in online scenarios
- Measures social welfare metrics
- Validates adaptive behavior

#### 2. Plan-based Evaluation (`test_plan_sw_exp2.m`)
- Evaluates different planning strategies
- Measures plan effectiveness
- Compares resource utilization

#### 3. Query-based Evaluation (`test_query_sw_exp3.m`, `test_query_cost_exp4.m`)
- Analyzes query performance
- Measures query costs
- Evaluates optimization effectiveness

#### 4. Budget-based Evaluation (`test_budget_sw_exp5.m`)
- Tests budget constraints impact
- Validates system components

#### 5. Abalation Study (`test_ablation_exp6.m`)
- Tests the impact of greedy strategies
- Performs ablation studies


## Integration Examples

### Apache Flink Integration
```java
public class OSTORResourceManager extends DefaultResourceManager {
    @Override
    public void onResourceAvailable(ResourceID resourceId) {
        // Interface with OSTOR for optimal resource allocation
        OSTORScheduler.allocateResource(resourceId);
    }
    
    @Override
    public void onStreamStateChange(StreamState state) {
        // Adapt resource allocation based on stream state
        updateAllocation(state);
    }
}
```

### Custom Stream Processing System
```python
class StreamProcessor:
    def __init__(self):
        self.resource_manager = OSTORManager()
        self.query_optimizer = QueryOptimizer()
        
    def process_stream(self, stream_data):
        # Get optimal resource allocation
        allocation = self.resource_manager.get_optimal_allocation()
        
        # Optimize query execution plan
        plan = self.query_optimizer.optimize(stream_data, allocation)
        
        # Execute with optimized allocation
        return self.execute_with_allocation(stream_data, plan)
        
    def monitor_performance(self):
        # Collect performance metrics
        metrics = self.collect_metrics()
        
        # Adjust allocation if needed
        self.resource_manager.adjust_allocation(metrics)
```

## Performance Tuning

### Configuration Parameters
```matlab
% System configuration
config.zeta = 0.7;          % Learning rate
config.threshold = 0.8;     % Utilization threshold
config.window_size = 100;   % Monitoring window size

% Resource management parameters
config.min_resources = 10;  % Minimum resource allocation
config.max_resources = 100; % Maximum resource allocation
```


## Requirements

- MATLAB R2020a or later
- Compatible with major stream processing frameworks
- Minimum 8GB RAM for experimental validation
- Python 3.7+ (for custom integration)
- Java 8+ (for Flink integration)

## Getting Started

1. Clone the repository
```bash
git clone https://github.com/JennieCheng/OSTOR.git
```

2. Configure system parameters
```matlab
% Edit config/settings.m
config.system.parameters = your_parameters;
```

3. Run integration tests
```bash
matlab -nodisplay -nosplash -nodesktop -r "run_integration_tests"
```

4. Validate installation
```matlab
run_validation_suite
```

## Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

