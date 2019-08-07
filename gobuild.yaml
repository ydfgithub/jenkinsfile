apiVersion: devops.alauda.io/v1alpha1
kind: ClusterPipelineTemplate
metadata:
  annotations:
    alauda.io/description.en: Clone -> Golang Build -> Docker Build
    alauda.io/description.zh-CN: 克隆代码 -> Golang 构建 -> Docker 构建
    alauda.io/displayName.en: Golang Build
    alauda.io/displayName.zh-CN: Golang 构建
    alauda.io/style.icon: golang,docker,sonarqube
    alauda.io/version: 2.0.0
    templateName: GoLangBuilder
  labels:
    category: Build
    source: official
    templateName: GoLangBuilder
  name: GoLangBuilder.2.0.0
  resourceVersion: "2661"
  selfLink: /apis/devops.alauda.io/v1alpha1/clusterpipelinetemplates/GoLangBuilder.2.0.0
  uid: 6093da43-b660-11e9-94cb-0a580ac700d8
spec:
  agent:
    label: golang
    raw: ""
  arguments:
  - displayName:
      en: Clone
      zh-CN: 代码检出
    items:
    - binding:
      - clone.args.PlatformCodeRepository
      - sonar.args.PlatformCodeRepository
      default: ""
      display:
        description:
          en: please select a code repository
          zh-CN: 选择已为项目分配的代码仓库
        name:
          en: RepositoryPath
          zh-CN: 代码仓库
        type: alauda.io/coderepositorymix
      name: PlatformCodeRepository
      required: true
      schema:
        type: alauda.io/coderepositorymix
      value: ""
    - binding:
      - clone.args.Branch
      - sonar.args.Branch
      default: ""
      display:
        description:
          en: The code repository branch that you want to check out.
          zh-CN: 检出代码仓库中的分支
        name:
          en: Branch
          zh-CN: 分支
        related: PlatformCodeRepository
        type: alauda.io/codebranch
      name: Branch
      required: true
      schema:
        type: string
      value: ""
    - binding:
      - clone.args.RelativeDirectory
      default: src
      display:
        description:
          en: Used as the path in GOPATH, e.g src/github.com/alauda/alauda. Specify
            a local directory (relative to the workspace root) where the Git repository
            will be checked out. If left empty, the workspace root itself will be
            used
          zh-CN: 在 Golang 程序为 GOPATH的子目录，例如 src/github.com/alauda/alauda。指定检出 Git
            仓库的本地目录(相对于 workspace 根目录)。若为空，将使用 workspace 根目录
        name:
          en: Relative Directory
          zh-CN: 相对目录
        type: string
      name: RelativeDirectory
      required: true
      schema:
        type: string
      value: ""
  - displayName:
      en: Golang Build
      zh-CN: Golang 构建
    items:
    - binding:
      - golang.args.buildCommand
      default: go build
      display:
        description:
          en: 'build command. Defaults to: go build'
          zh-CN: 自定义更详细的构建命令。默认为：go build
        name:
          en: Build Command
          zh-CN: 构建命令
        type: code
      name: buildCommand
      required: true
      schema:
        type: string
      value: ""
  - displayName:
      en: Code Scanning
      zh-CN: 代码扫描
    items:
    - binding: null
      default: ""
      display:
        description:
          en: Whether to use Sonarqube for code scan
          zh-CN: 开启后，进行代码扫描
        name:
          en: Use code analysis
          zh-CN: 开启代码扫描
        type: boolean
      name: UseSonarQube
      required: false
      schema:
        type: boolean
      value: "false"
    - binding:
      - sonar.args.CodeQualityBinding
      default: ""
      display:
        args:
          bindingKind: codequalitytool
          bindingToolType: Sonarqube
        description:
          en: Select a SonarQube instance
          zh-CN: 选择要使用的 SonarQube 实例
        name:
          en: SonarQube instance
          zh-CN: SonarQube 实例
        type: alauda.io/toolbinding
      name: CodeQualityBinding
      relation:
      - action: show
        when:
          name: UseSonarQube
          value: true
      required: true
      schema:
        type: alauda.io/toolbinding
      value: ""
    - binding:
      - sonar.args.EnableBranchAnalysis
      default: ""
      display:
        advanced: true
        description:
          en: When scanning branches other than the main branch while keeping separate
            results, the Sonarqube instance needs to support branch analysis and turn
            on this feature
          zh-CN: 扫描主分支以外的分支时，若想查看这些分支的扫描结果，需要在Sonarqube 支持多代码分支的同时，开启此开关
        name:
          en: Enable branch analysis
          zh-CN: 区分代码分支
        type: boolean
      name: EnableBranchAnalysis
      relation:
      - action: show
        when:
          name: UseSonarQube
          value: true
      required: false
      schema:
        type: boolean
      value: "false"
    - binding:
      - sonar.args.AnalysisParameters
      default: ""
      display:
        description:
          en: Set analysis parameters for Sonar Scanner. When 'sonar-project.properties'
            file exists in the code repository, this argument will be omitted. See
            https://docs.sonarqube.org/latest/analysis/analysis-parameters and https://docs.sonarqube.org/display/PLUG/SonarGo
          zh-CN: '为 Sonar Scanner 设置分析参数。当目录中存在 sonar-project.properties 文件时，将会忽略这个参数。详细参数见文档:
            https://docs.sonarqube.org/latest/analysis/analysis-parameters 和 https://docs.sonarqube.org/display/PLUG/SonarGo'
        name:
          en: Analysis Parameters
          zh-CN: 代码扫描参数
        type: stringMultiline
      name: AnalysisParameters
      relation:
      - action: show
        when:
          name: UseSonarQube
          value: true
      required: false
      schema:
        type: string
      value: |
        sonar.sources=.
        sonar.sourceEncoding=UTF-8
    - binding:
      - sonar.args.FailedIfNotPassQualityGate
      default: ""
      display:
        advanced: true
        description:
          en: Fails pipeline execution when quality gate fails
          zh-CN: 开启后，代码扫描结果为失败时，流水线执行状态变为失败，终止流水线
        name:
          en: Fail pipeline when quality gate fails
          zh-CN: 质量阈未通过终止流水线
        type: boolean
      name: FailedIfNotPassQualityGate
      relation:
      - action: show
        when:
          name: UseSonarQube
          value: true
      required: false
      schema:
        type: boolean
      value: "false"
  - displayName:
      en: Docker Build
      zh-CN: Docker 构建
    items:
    - binding:
      - build-docker.args.imageRepository
      default: ""
      display:
        description:
          en: please select a image repository or input an image repository address
          zh-CN: 选择已为项目分配的镜像仓库或者输入地址
        name:
          en: Repository
          zh-CN: 镜像仓库
        type: alauda.io/dockerimagerepositorymix
      name: imageRepository
      required: true
      schema:
        type: alauda.io/dockerimagerepositorymix
      value: ""
    - binding:
      - build-docker.args.context
      default: .
      display:
        advanced: true
        description:
          en: The build process can refer to any of the files in the context. For
            example, your build can use a COPY instruction to reference a file in
            the context
          zh-CN: 构建过程可以引用上下文中的任何文件。例如，构建中可以使用 COPY 命令在上下文中引用文件
        name:
          en: Build Context
          zh-CN: 构建上下文
        type: string
      name: context
      required: true
      schema:
        type: string
      value: ""
    - binding:
      - build-docker.args.buildArguments
      default: ""
      display:
        advanced: true
        description:
          en: docker build arguments
          zh-CN: 自定义更多的构建参数，对镜像构建进行更详细的配置
        name:
          en: Build Arguments
          zh-CN: 构建参数
        type: string
      name: buildArguments
      required: false
      schema:
        type: string
      value: ""
    - binding:
      - build-docker.args.dockerfile
      default: Dockerfile
      display:
        advanced: true
        description:
          en: Dockerfile absolute path
          zh-CN: Dockerfile 在代码仓库中的绝对路径
        name:
          en: Dockerfile
          zh-CN: Dockerfile
        type: string
      name: dockerfile
      required: true
      schema:
        type: string
      value: ""
    - binding:
      - build-docker.args.retry
      default: "3"
      display:
        advanced: true
        description:
          en: number of retries when building docker image
          zh-CN: 生成镜像时的失败重试次数
        name:
          en: Retry Times
          zh-CN: 重试次数
        type: string
      name: retry
      required: false
      schema:
        type: string
      value: ""
  engine: graph
  options:
    timeout: 0
  stages:
  - display:
      en: Clone
      zh-CN: Clone
    name: Clone
    tasks:
    - display:
        en: clone
        zh-CN: clone
      kind: ClusterPipelineTaskTemplate
      name: clone.2.0.0
      type: public/clone
  - display:
      en: Golang Build
      zh-CN: Golang Build
    name: Golang Build
    tasks:
    - display:
        en: golang
        zh-CN: golang
      kind: ClusterPipelineTaskTemplate
      name: golang.2.0.0
      type: public/golang
  - display:
      en: Code Scan
      zh-CN: Code Scan
    name: Code Scan
    tasks:
    - display:
        en: sonar
        zh-CN: sonar
      kind: ClusterPipelineTaskTemplate
      name: sonar.2.0.1
      relation:
      - action: show
        when:
          name: UseSonarQube
          value: true
      type: public/sonar
  - display:
      en: Docker Build
      zh-CN: Docker Build
    name: Docker Build
    tasks:
    - display:
        en: build-docker
        zh-CN: build-docker
      kind: ClusterPipelineTaskTemplate
      name: build-docker.2.0.0
      type: public/build-docker
  triggers:
    raw: ""
  values: {}
  withSCM: true
