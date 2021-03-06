# Paperclip with Hobo

Install this plugin alongside [paperclip](http://jimneath.org/2008/04/17/paperclip-attaching-files-in-rails/).

It adds two small things:

 - Automatically declares the fields for you, so you can just add

        has_attached_file :photo

   to your model, and then run the migration generator to add the `photo_file_name`, `photo_content_type`, `photo_file_size` and `photo_updated_at` fields to the table.

 - Declares an input field

        <def tag="input" for="Paperclip::Attachment">
          <%= file_field_tag param_name_for_this, attributes %>
        </def>

    (to get this, you need `<include src="paperclip" plugin="paperclip_with_hobo" />` in application.dryml)

To get your file upload actually running don't forget to define the form:

    <def tag="form" for="User">
      <form merge multipart param="default">
        <error-messages param/>
        <field-list fields="photo" param/>
        <div param="actions">
          <submit label="Save" param/><or-cancel param="cancel"/>
        </div>
      </form>
    </def>

`<form>` must be instructed to create a `multipart` form and the `<field-list>` must include the same attachment field which you defined by `has_attached_file :photo` in your model.

Don't forget to include all the other fields you want to display in the form and last but not least replace `User` with your actual model.

## Important Note

The name of the plugin is important. It doesn't *have* to be `paperclip_with_hobo` but it will only work if this plugin loads *after* paperclip itself. Calling it `paperclip_something` is a good way to ensure that.