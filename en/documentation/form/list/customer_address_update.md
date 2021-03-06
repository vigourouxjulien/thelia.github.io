---
layout: form
title: customer update address
form_name: thelia.front.address.update
sidebar: form
subnav: form_list_addressupdate
fields:
    - { name: "label", mandatory: "true", description: "label for identifying the address"}
    - { name: "title", mandatory: "true", description: "customer title ID. See [title loop](http://doc.thelia.net/en/documentation/loop/title.html)"}
    - { name: "firstname", mandatory: "true", description: "customer first name"}
    - { name: "lastname", mandatory: "true", description: "customer last name"}
    - { name: "address1", mandatory: "true", description: "customer street address"}
    - { name: "address2", mandatory: "false", description: "customer street address complement"}
    - { name: "address3", mandatory: "false", description: "customer street address complement"}
    - { name: "zipcode", mandatory: "true", description: "customer zip code"}
    - { name: "city", mandatory: "true", description: "customer city"}
    - { name: "country", mandatory: "true", description: "customer country id"}
    - { name: "phone", mandatory: "false", description: "customer phone"}
    - { name: "cellphone", mandatory: "false", description: "customer cell phone"}
    - { name: "is_default", mandatory: "false", description: "send this parameter to true if the address is the default one"}
lang: en

---
```
{form name="thelia.front.address.update"}
{loop name="customer.update" type="address" customer="current" id="{$address_id}"}
    <form id="form-address" class="form-horizontal" action="{url path="/address/update/{$address_id}"}" method="post">
    {form_field form=$form field='success_url'}
        <input type="hidden" name="{$name}" value="{url path="/account"}" />
    {/form_field}

    {form_field form=$form field='error_message'}
        <input type="hidden" name="{$name}" value="{intl l="missing or invalid data"}" />
    {/form_field}
    {form_hidden_fields form=$form}
    {if $form_error}<div class="alert alert-danger">{$form_error_message}</div>{/if}
    <fieldset class="panel">
        <div class="panel-heading">
            {intl l="Address"}
        </div>

        <div class="panel-body">
            {form_field form=$form field="label"}
                <div class="form-group group-label{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$LABEL}}" id="{$label_attr.for}" class="form-control" minlength="2" maxlength="255" placeholder="{intl l="Placeholder address label"}"{if $required} aria-required="true" required{/if}{if !$value || $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {elseif !$value}
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="title"}
                {assign var="customer_title_id" value="{$value|default:$TITLE}"}
                <div class="form-group group-title{if $error} has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <select name="{$name}" id="{$label_attr.for}" class="form-control"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                            <option value="">-- {intl l="Select Title"} --</option>
                            {loop type="title" name="title.list"}
                                <option value="{$ID}" {if $customer_title_id == $ID}selected{/if}>{$LONG}</option>
                            {/loop}
                        </select>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="firstname"}
                <div class="form-group group-firstname {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$FIRSTNAME} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder firstname"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}
            <!--/.form-group-->

            {form_field form=$form field="lastname"}
                <div class="form-group group-lastname {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$LASTNAME} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder lastname"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="company"}
              <div class="form-group group-company{if $error} has-error{/if}">
                <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>
                  <div class="control-input">
                    <input type="text" name="{$name}" value="{$value|default:{$COMPANY} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder company"}" value="{$value}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                    {if $error }
                      <span class="help-block">{$message}</span>
                      {assign var="error_focus" value="true"}
                    {/if}
                  </div>
              </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="address1"}
                <div class="form-group group-address1 {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$ADDRESS1} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder address1"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="address2"}
                <div class="form-group group-address2 {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if} </label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$ADDRESS2} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder address2"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="zipcode"}
                <div class="form-group group-zipcode {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$ZIPCODE}}" id="{$label_attr.for}" class="form-control" maxlength="10" placeholder="{intl l="Placeholder zipcode"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="city"}
                <div class="form-group group-city {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$CITY} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="255" placeholder="{intl l="Placeholder city"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="country"}
                {assign var="customer_country_id" value="{$value|default:$COUNTRY}"}
                <div class="form-group group-country {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>
                    <div class="control-input">
                        <select name="{$name}" id="{$label_attr.for}" class="form-control"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                            <option value="">-- {intl l="Select Country"} --</option>
                            {loop type="country" name="country.list"}
                                <option value="{$ID}" {if $customer_country_id == $ID}selected{/if}>{$TITLE}</option>
                            {/loop}
                        </select>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div><!--/.form-group-->
            {/form_field}

            {form_field form=$form field="phone"}
                <div class="form-group group-phone {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$PHONE} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="20" placeholder="{intl l="Placeholder phone"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}

            {form_field form=$form field="cellphone"}
                <div class="form-group group-cellphone {if $error}has-error{/if}">
                    <label class="control-label" for="{$label_attr.for}">{$label}:{if $required} <span class="required">*</span>{/if}</label>

                    <div class="control-input">
                        <input type="text" name="{$name}" value="{$value|default:{$CELLPHONE} nofilter}" id="{$label_attr.for}" class="form-control" maxlength="20" placeholder="{intl l="Placeholder cellphone"}"{if $required} aria-required="true" required{/if}{if !isset($error_focus) && $error} autofocus{/if}>
                        {if $error }
                            <span class="help-block">{$message}</span>
                            {assign var="error_focus" value="true"}
                        {/if}
                    </div>
                </div>
                <!--/.form-group-->
            {/form_field}
        </div>
    </fieldset>

    {form_field form=$form field="is_default"}
        {if not $DEFAULT}
        <div class="form-group group-primary">
            <div class="control-input">
                <div class="checkbox">
                    <label class="control-label" for="{$label_attr.for}">
                        <input type="checkbox" name="{$name}" id="{$label_attr.for}" value="1"> {$label}
                    </label>
                </div>
            </div>
        </div>
        <!--/.form-group-->
        {/if}
    {/form_field}

    <div class="form-group group-btn">
        <div class="control-btn">
            <button type="submit" class="btn btn-submit">{intl l="Update"}</button>
        </div>
    </div>
    <!--/.form-group-->
    </form>
    {/loop}
{/form}
```