FROM quay.io/kubevirtci/bootstrap:v20210715-d0c2b78

RUN set -x && \
    git clone https://github.com/kubernetes/test-infra.git && \
    cd ./test-infra && \
    git checkout 00bc5aa56077a37432ce757dbae358c56435c010 && \
    bazel build //robots/pr-creator:pr-creator && \
    cp ./bazel-out/k8-fastbuild/bin/robots/pr-creator/pr-creator_/pr-creator /usr/local/bin && \
    chmod +x /usr/local/bin/pr-creator && \
    bazel clean --expunge && \
    cd .. && rm -rf ./test-infra

RUN set -x && \
    git clone https://github.com/kubevirt/project-infra.git && \
    cd ./project-infra && \
    cp ./hack/git-askpass.sh hack/git-pr.sh /usr/local/bin && \
    chmod +x /usr/local/bin/git-askpass.sh /usr/local/bin/git-pr.sh && \
    bazel build //robots/cmd/labels-checker:labels-checker && \
    cp ./bazel-out/k8-fastbuild/bin/robots/cmd/labels-checker/labels-checker_/labels-checker /usr/local/bin && \
    chmod +x /usr/local/bin/labels-checker && \
    cd .. && rm -rf ./project-infra

ENV GIT_ASKPASS=/usr/local/bin/git-askpass.sh
