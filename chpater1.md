# Build a REST API with Spring and Java Config

## 1. 개요

This chapter shows how to set up REST in Spring – the Controller and HTTP response codes,
configuration of payload marshalling and content negotiation.

이 장에서는 Spring에서 REST API를 어떻게 설정하는지 보여준다. 컨트롤러와 HTTP 응답 코드의 설정, 페이로드를 변환하는 방식(payload marshalling), 그리고 클라이언트와 서버 간 콘텐츠 형식을 조율하는 content negotiation 설정까지 포함된다.

## 2. 스프링 내에서의 REST 이해

The Spring framework supports two ways of creating RESTful services

- using MVC with ModelAndView
- using HTTP message converters

The ModelAndView approach(접근) is older and much better documented, but also more verbose(장황한)and configuration heavy. It tries to shoehorn(억지로 끼워 넣다) the REST paradigm into the old model, which is not without problems. The Spring team understood this and provided first-class REST support starting with Spring 3.0.

The new approach, based on HttpMessageConverter and annotations, is much more
lightweight and easy to implement. Configuration is minimal, and it provides sensible(합리적인) defaults for what you would expect from a RESTful service.

스프링 프레임워크는 RESTful 서비스 생성하는 두개의 방식을 지원한다.

- MVC 사용방식(ModelAndView 기반)
- HTTP 메세지 컨버터 방식

ModelAndView 방식은 오래된 방법으로, 문서가 잘 갖춰져 있지만 장황하고 설정이 복잡하다. 이 방식은 REST 패러다임을 기존 모델에 억지로 끼워 맞추려 해서 여러 문제점이 있다. 이러한 점을 스프링 팀이 인지하여 Spring 3.0부터 본격적인 REST 지원을 시작했다.

새로운 방식은 HttpMessageConverter와 어노테이션을 기반으로 하며, 훨씬 가볍고 구현이 쉽다. 설정이 최소화되어 있고, RESTful 서비스에 기대하는 기본 기능들을 합리적인 디폴트로 제공한다.

## 3. The Java Configuration

```java

@Configuration
@EnableWebMvc
public class WebConfig{

}
```

The new @EnableWebMvc annotation does some useful things – specifically(구체적으로), in the case of
REST, it detects the existence of Jackson and JAXB 2 on the classpath and automatically
creates and registers default JSON and XML converters. The functionality of the annotation is
equivalent to the XML version:

`<mvc:annotation-driven />`

This is a shortcut, and though it may be useful in many situations, it’s not perfect.
When more complex configuration is needed, remove the annotation and extend
WebMvcConfigurationSupport directly

새로운 @EnableWebMvc 어노테이션은 REST 환경에서 Jackson과 JAXB 2가 클래스패스에 있을 경우 이를 감지하여 기본 JSON과 XML 컨버터를 자동으로 생성하고 등록해줍니다.
이 어노테이션의 기능은 XML 설정의 <mvc:annotation-driven />과 동일합니다.

요약하자면, 간단한 설정에는 이 어노테이션이 편리하지만, 더 복잡한 설정이 필요할 때는 @EnableWebMvc를 제거하고 WebMvcConfigurationSupport를 직접 확장해서 사용해야 합니다.

## 3.1. Using Spring Boot

If we’re using the @SpringBootApplication annotation and the spring-webmvc library is on the
classpath, then the @EnableWebMvc annotation is added automatically with
a default autoconfiguration.
We can still add MVC functionality to this configuration by implementing the
WebMvcConfigurer interface on a @Configuration annotated class. We can also use a
WebMvcRegistrationsAdapter instance to provide our own RequestMappingHandlerMapping,
RequestMappingHandlerAdapter, or ExceptionHandlerExceptionResolver implementations.
Finally, if we want to discard Spring Boot’s MVC features and declare a custom configuration,
we can do so by using the @EnableWebMvc annotation.

@SpringBootApplication 어노테이션을 사용하고 spring-webmvc 라이브러리가 클래스패스에 포함되어 있으면, @EnableWebMvc 어노테이션이 자동으로 적용되어 기본 자동 설정이 활성화됩니다.
추가로 MVC 기능을 확장하고 싶다면, @Configuration이 붙은 클래스에서 WebMvcConfigurer 인터페이스를 구현할 수 있습니다.
또한, WebMvcRegistrationsAdapter를 활용해 직접 RequestMappingHandlerMapping, RequestMappingHandlerAdapter, ExceptionHandlerExceptionResolver 구현체를 제공할 수도 있습니다.
마지막으로, 스프링 부트의 MVC 기본 기능을 무시하고 완전히 커스텀 설정을 선언하고 싶을 경우에는 @EnableWebMvc 어노테이션을 명시적으로 붙여 사용하면 됩니다.
