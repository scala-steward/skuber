<p align="center"> <img src="docs/skuber_logo.png" alt="skuber logo"> </p>

<p align="center"> Scala client for the <a href="https://kubernetes.io/" target="_blank">Kubernetes API</a>. </p>

</br>
<p align="center">
  <img src="https://img.shields.io/github/release-date/hagay3/skuber?style=for-the-badge" alt="Latest release date" />
<a href="https://mvnrepository.com/artifact/io.github.hagay3/skuber_2.12" target="_blank">
    <img src="https://img.shields.io/maven-central/v/io.github.hagay3/skuber_2.12?color=green&style=for-the-badge" alt="Maven Central" />
  </a>
  <a href="https://discord.gg/byEh56vFJR" target="_blank">
    <img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord" />
  </a>
</p>



<p align="center">
  <strong>
  <a href="https://hagay3.github.io/skuber/" target="_blank">Read the Documentation</a>.
  </strong>
 </p>

</br>

## Quick start

This example lists pods in `kube-system` namespace:

  ```scala
  import skuber._
  import skuber.json.format._
  import org.apache.pekko.actor.ActorSystem
  import scala.util.{Success, Failure}

  implicit val system = ActorSystem()
  implicit val dispatcher = system.dispatcher

  val k8s = k8sInit
  val listPodsRequest = k8s.list[PodList](Some("kube-system"))
  listPodsRequest.onComplete {
    case Success(pods) => pods.items.foreach { p => println(p.name) }
    case Failure(e) => throw(e)
  }
  ```

## Documentation
Read the [documentation](https://hagay3.github.io/skuber/#/) and join [discord community](https://discord.gg/byEh56vFJR) to  ask your questions!


## Features
- Uses standard `kubeconfig` files for configuration - see the [configuration guide](https://hagay3.github.io/skuber/#/?id=configuration) for details
- Scala 3.2, 2.13, 2.12 support
- [Typed Kubernetes Client](https://hagay3.github.io/skuber/#/?id=basic-imports) for creating, reading, updating, removing, listing and watching resources on a Kubernetes cluster.
- [Dynamic Kubernetes Client](https://hagay3.github.io/skuber/#/?id=dynamic-kubernetes-client), which allows you to interact with Kubernetes API without strict types.
- Refreshing EKS tokens [Refresh EKS Token guide](https://hagay3.github.io/skuber/#/?id=refresh-eks-aws-token)
- Comprehensive support for Kubernetes API model represented as Scala case classes
- Support for core, extensions and other Kubernetes API groups
- Full support for converting resources between the case class and standard JSON representations
- The API is asynchronous and strongly typed e.g. `k8s get[Deployment]("nginx")` returns a value of type `Future[Deployment]`
- Fluent API for creating and updating specifications of Kubernetes resources



## Prerequisites

- Java 17
- Kubernetes cluster

A Kubernetes cluster is needed at runtime. For local development purposes, minikube is recommended.
To get minikube follow the instructions [here](https://github.com/kubernetes/minikube)

## Release

You can use the latest release by adding to your build:
- Scala 3.2, 2.13, 2.12 support

```sbt
libraryDependencies += "io.github.hagay3" %% "skuber" % "4.0.2"
```

## Building

Building the library from source is very straightforward. Simply run `sbt test` in the root directory of the project to build the library (and examples) and run the unit tests to verify the build.

## CI + Build
The CI parameters defined in `build.sbt`.

ci.yaml and clean.yaml are generated automatically with [sbt-github-actions](https://github.com/djspiewak/sbt-github-actions) plugin.  

Run `sbt githubWorkflowGenerate && bash infra/ci/fix-workflows.sh` in order to regenerate ci.yaml and clean.yaml.

CI Running against the following k8s version
* v1.24.1

skuber supports all other k8s versions, not all of them tested under CI.

https://kubernetes.io/releases/


## Support
I'm trying to be responsive to any new issues, you can create github issue or contact me.

Skuber chat on discord: https://discord.gg/byEh56vFJR 

Email: hagay3@gmail.com
