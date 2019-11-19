# Android Rule
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "build_bazel_rules_android",
    urls = ["https://github.com/bazelbuild/rules_android/archive/v0.1.1.zip"],
    sha256 = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806",
    strip_prefix = "rules_android-0.1.1",
)

# Kotlin Rule
rules_kotlin_version = "sq_03"
rules_kotlin_sha = "10265479cc5044212dc3c47f18a18a7496399ee496b0da187d41f1720fa8e555"
http_archive(
    name = "io_bazel_rules_kotlin",
    urls = ["https://github.com/cgruber/rules_kotlin/archive/%s.zip" % rules_kotlin_version],
    type = "zip",
    strip_prefix = "rules_kotlin-%s" % rules_kotlin_version,
    sha256 = rules_kotlin_sha,
)

KOTLIN_VERSION = "1.3.20"
KOTLINC_RELEASE_SHA = "2d505fb505c53db7fc6a2a570d97ba3b7a6d3526d4f64aee28de6fda7502f3f0"

KOTLINC_RELEASE = {
    "urls": [
        "https://github.com/JetBrains/kotlin/releases/download/v{v}/kotlin-compiler-{v}.zip".format(v = KOTLIN_VERSION),
    ],
    "sha256": KOTLINC_RELEASE_SHA,
}

load("@io_bazel_rules_kotlin//kotlin:kotlin.bzl", "kotlin_repositories", "kt_register_toolchains")
kotlin_repositories(compiler_release = KOTLINC_RELEASE)
kt_register_toolchains() # to use the default toolchain, otherwise see toolchains below

# Maven Rule
RULES_JVM_EXTERNAL_TAG = "2.8"
RULES_JVM_EXTERNAL_SHA = "79c9850690d7614ecdb72d68394f994fef7534b292c4867ce5e7dec0aa7bdfad"

http_archive(
    name = "rules_jvm_external",
    strip_prefix = "rules_jvm_external-%s" % RULES_JVM_EXTERNAL_TAG,
    sha256 = RULES_JVM_EXTERNAL_SHA,
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/%s.zip" % RULES_JVM_EXTERNAL_TAG,
)

load("@rules_jvm_external//:defs.bzl", "maven_install")
load("//tools/bazel/rules:dependencies.bzl", "COMMONLIBS", "TESTLIBS")

maven_install(
    artifacts = COMMONLIBS + TESTLIBS,
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
        "https://jcenter.bintray.com",
    ],
    excluded_artifacts = [
        "com.google.guava:guava", # excludes guava-jre
    ],
)

# Robolectric
http_archive(
    name = "robolectric",
    urls = ["https://github.com/robolectric/robolectric-bazel/archive/4.0.1.tar.gz"],
    strip_prefix = "robolectric-bazel-4.0.1",
    sha256 = "dff7a1f8e7bd8dc737f20b6bbfaf78d8b5851debe6a074757f75041029f0c43b",
)
load("@robolectric//bazel:robolectric.bzl", "robolectric_repositories")
robolectric_repositories()

http_archive(
    name = "google_bazel_common",
    strip_prefix = "bazel-common-f54045d200b6141f309ce59f9c8397ac0ef2f98c",
    urls = ["https://github.com/changusmc/bazel-common/archive/f54045d200b6141f309ce59f9c8397ac0ef2f98c.zip"],
)

load("@google_bazel_common//:workspace_defs.bzl", "google_common_workspace_rules")

google_common_workspace_rules(28, "28.0.3")
