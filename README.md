# Opencensus Ktor

This is a Ktor Server and Client feature to integrate Opencensus Tracing in your web application.

All the HTTP attributes and MessageEvent for HTTP are created for you and propagated.

## Usage
```kotlin
install(OpencensusTracingServer) {
    traceSampler = Samplers.alwaysSample()
    ignoredPath = listOf("/health")
    exporterSetup = {
        StackdriverTraceExporter.createAndRegister(
            StackdriverTraceConfiguration.builder()
                .build()
        )
    }
}
```
 * The default sampler is a probability sampler, sampling 1/1000 trace.
 * `ignorePath` is a list of path that should not be traced. You can simlpy put the beginning of a path to ignore all the sub paths, for example `"/users"` would make it also ignore `"/users/bob"`.
 * `exporterSetup` is a block of code to instantiate the Opencensus exporter you need.
