###### Этапы поднятия контекста:
1. Парсирование конфигурации
2. Настройка созданных BeanDefinition (BeanFactoryPostPrpcessor)
3. Создание кастомных FactoryBean (FactoryBean<T>)
4. BeanFactory создает экземпляры бинов, при необходимости делегируя создание FactoryBean (BeanFactory)
5. Настройка созданных бинов (BeanPostProcessor)

###Первый этап
Цель первого этапа — это создание всех BeanDefinition.

_BeanDefinition_ — это специальный интерфейс, через который можно получить доступ к метаданным будущего бина
Содержит след-ю информацию:
- scope
- lazy(true/false)
- BeanClassName
- getDependsOn (список бинов, от которого зависит этот бин)
- init/destroy methods


**_ClassPathBeanDefinitionScanner**_ - сканирует указанный пакет в поисках бинов,
помеченных аннотацией @Component и наследников. Чтобы сканирование было запущено, в конфигурации должен быть указан пакет для
сканирования с помощью @ComponentScan.

**_AnnotatedBeanDefinitionReader_** работает в несколько этапов
1. Регистрация всех классов, помеченных аннотацией @Configuration
2. Регистрация BeanDefinitionRegistryPostProcessor, который парсирует JavaConfig и создает BeanDefinition


###Второй этап

BeanFactoryPostProcessor - позволяет влиять на bean-ы еще до того как они будут созданы
Например, инжектить параметры, которые хранятся в app.yaml файлах

###Третий этап

FactoryBean — это generic интерфейс, которому можно делегировать процесс создания бинов типа<T>.

### Четвертый этап

Созданием экземпляров бинов занимается BeanFactory при этом, если нужно, делегирует это кастомным FactoryBean. 
Экземпляры бинов создаются на основе ранее созданных BeanDefinition и добавляются в мапу <BeanName, Bean>

###Пятый этап

Интерфейс BeanPostProcessor позволяет вклиниться в процесс настройки ваших бинов до того, как они попадут в контейнер. Интерфейс несет в себе несколько методов:
- postProcessBeforeInitialization
  (между ними postConstruct, до того, как настроены все прокси)
- postProcessAfterInitialization

Если вы хотите сделать прокси над вашим объектом, то имейте ввиду, что это принято делать после вызова init метода, иначе говоря это нужно делать в методе postProcessAfterInitialization.


