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
