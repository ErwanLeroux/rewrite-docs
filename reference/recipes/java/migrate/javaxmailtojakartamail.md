# Migrate deprecated `javax.mail` packages to `jakarta.mail`

** org.openrewrite.java.migrate.JavaxMailToJakartaMail**
_Java EE has been rebranded to Jakarta EE, necessitating a package relocation._

## Source

[Github](https://github.com/openrewrite/rewrite-migrate-java), [Issue Tracker](https://github.com/openrewrite/rewrite-migrate-java/issues), [Maven Central](https://search.maven.org/artifact/org.openrewrite.recipe/rewrite-migrate-java/1.8.0/jar)

* groupId: org.openrewrite.recipe
* artifactId: rewrite-migrate-java
* version: 1.8.0


## Usage

This recipe has no required configuration options and can be activated directly after taking a dependency on org.openrewrite.recipe:rewrite-migrate-java:1.8.0 in your build file:

{% tabs %}
{% tab title="Gradle" %}
{% code title="build.gradle" %}
```groovy
plugins {
    id("org.openrewrite.rewrite") version("5.25.0")
}

rewrite {
    activeRecipe("org.openrewrite.java.migrate.JavaxMailToJakartaMail")
}

repositories {
    mavenCentral()
}

dependencies {
    rewrite("org.openrewrite.recipe:rewrite-migrate-java:1.8.0")
}
```
{% endcode %}
{% endtab %}

{% tab title="Maven" %}
{% code title="pom.xml" %}
```markup
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>org.openrewrite.maven</groupId>
        <artifactId>rewrite-maven-plugin</artifactId>
        <version>4.30.0</version>
        <configuration>
          <activeRecipes>
            <recipe>org.openrewrite.java.migrate.JavaxMailToJakartaMail</recipe>
          </activeRecipes>
        </configuration>
        <dependencies>
          <dependency>
            <groupId>org.openrewrite.recipe</groupId>
            <artifactId>rewrite-migrate-java</artifactId>
            <version>1.8.0</version>
          </dependency>
        </dependencies>
      </plugin>
    </plugins>
  </build>
</project>
```
{% endcode %}
{% endtab %}
{% endtabs %}

Recipes can also be activated directly from the command line by adding the argument `-Drewrite.activeRecipesorg.openrewrite.java.migrate.JavaxMailToJakartaMail`

## Definition

{% tabs %}
{% tab title="Recipe List" %}
* [Add Maven dependency](../../maven/adddependency.md)
  * groupId: `jakarta.mail`
  * artifactId: `jakarta.mail-api`
  * version: `2.x`
  * onlyIfUsing: `javax.mail.*`
* [Upgrade Maven dependency version](../../maven/upgradedependencyversion.md)
  * groupId: `jakarta.mail`
  * artifactId: `jakarta.mail-api`
  * newVersion: `2.x`
* [Rename package name](../../java/changepackage.md)
  * oldPackageName: `javax.mail`
  * newPackageName: `jakarta.mail`
  * recursive: `true`
* [Remove Maven dependency](../../maven/removedependency.md)
  * groupId: `javax.mail`
  * artifactId: `javax.mail-api`

{% endtab %}

{% tab title="Yaml Recipe List" %}
```yaml
---
type: specs.openrewrite.org/v1beta/recipe
name: org.openrewrite.java.migrate.JavaxMailToJakartaMail
displayName: Migrate deprecated `javax.mail` packages to `jakarta.mail`
description: Java EE has been rebranded to Jakarta EE, necessitating a package relocation.
recipeList:
  - org.openrewrite.maven.AddDependency:
      groupId: jakarta.mail
      artifactId: jakarta.mail-api
      version: 2.x
      onlyIfUsing: javax.mail.*
  - org.openrewrite.maven.UpgradeDependencyVersion:
      groupId: jakarta.mail
      artifactId: jakarta.mail-api
      newVersion: 2.x
  - org.openrewrite.java.ChangePackage:
      oldPackageName: javax.mail
      newPackageName: jakarta.mail
      recursive: true
  - org.openrewrite.maven.RemoveDependency:
      groupId: javax.mail
      artifactId: javax.mail-api

```
{% endtab %}
{% endtabs %}